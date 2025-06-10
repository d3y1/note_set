# Nowcoder export solutions and convert to md files

牛客 https://www.nowcoder.com/

导出全部题解 转为md文件

<procedure>
   <step>
      <p>‌获取数据‌：requests(HTTP请求工具) → 发送请求获取网页HTML或者JSON返回值</p>
   </step>
   <step>
      <p>‌提取数据‌：BeautifulSoup(HTML/XML解析器) → 解析HTML，定位目标元素</p>
   </step>
   <step>
      <p>‌清洗数据‌：html2text(HTML转纯文本工具) → 将提取的HTML片段转为纯文本</p>
   </step>
</procedure>

```python

import requests
from bs4 import BeautifulSoup
import os
import html2text
import time

# 配置参数 从浏览器开发者工具获取
COOKIE = 'your_cookie'
USER_ID = 'your_userid'
# 最终md文件 保存目录
MD_FILE_DIR = '/xxx/yyy/zzz/target'
# 获取的所有题解id 保存目录
SOLUTION_ID_DIR = '/xxx/yyy/zzz/solutions'
# 获取的所有题解id 文件名称
SOLUTION_IDS_FILE = 'all_solution_ids.txt'

def get_all_solutions():
    session = requests.Session()
    session.headers.update({
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
    })
    
    all_solutions = []
    page = 1
    max_retry = 3
    
    # 每次获取一页 每页15个题解
    while True:
        try:
            timestamp_milliseconds = time.time_ns() // 1000000
            url = f"https://gw-c.nowcoder.com/api/sparta/user/content/my-content?pageNo={page}&userId={USER_ID}&_={timestamp_milliseconds}"
            print(f"----------------------当前页url: {url}\n")
            resp = session.get(url, timeout=10)
            resp.raise_for_status()
            print(f"----------------------当前页 15个题解: {resp.text}\n")

            # json中获取15个题解id
            solution_ids = [solution['contentId'] for solution in resp.json()['data']['records']]
            print(f"----------------------当前页 15个题解id: {solution_ids}\n")
            
            if not solution_ids:
                break
                
            all_solutions.extend(solution_ids)
            print(f"----------------------第{page}页: 获取完成!\n")
            page += 1
            time.sleep(2)
            
        except Exception as e:
            print(f"----------------------ERROR: {e}\n")
            max_retry -= 1
            if max_retry <= 0:
                break
            time.sleep(5)

    # 创建保存目录
    os.makedirs(SOLUTION_ID_DIR, exist_ok=True)
    # 保存所有题解id
    with open(f"{SOLUTION_ID_DIR}/{SOLUTION_IDS_FILE}", 'w', encoding='utf-8') as f:
        f.write(str(all_solutions))

    return all_solutions


def load_ids_from_txt(filepath):
    try:
        with open(filepath, 'r') as file:
            content = file.read().strip()  # 读取并去除首尾空格
            data_list = eval(content)      # 将字符串转为列表
            return data_list
    except FileNotFoundError:
        print(f"Error: File {filepath} not found")
        return []
    except SyntaxError:
        print("Error: Invalid list format in file")
        return []

def fetch_solutions():
    session = requests.Session()
    session.headers.update({'Cookie': COOKIE})

    # 方法1 直接API获取
    all_solutions = get_all_solutions()
    # 方法2 文件获取
    # all_solutions = load_ids_from_txt(f"{SOLUTION_ID_DIR}/{SOLUTION_IDS_FILE}")
    print(f"----------------------所有题解id: {all_solutions}")

    time.sleep(10)
    
    # 创建md文件保存目录
    os.makedirs(MD_FILE_DIR, exist_ok=True)
    
    for solution in all_solutions:
        print(f"----------------------当前题解id: {solution}")

        # 抓取单篇题解 示例: https://www.nowcoder.com/discuss/725120608257798144
        solution_url = f'https://www.nowcoder.com/discuss/{solution}'
        print(f"----------------------当前题解url: {solution_url}")
        detail_resp = session.get(solution_url)
        detail_soup = BeautifulSoup(detail_resp.text, 'html.parser')
        
        time.sleep(4)

        # 提取内容（需适配牛客网实际HTML结构）
        # 获取题解 标题
        title = detail_soup.find('p', class_='question-title')
        # 获取题解 刷题地址
        url = detail_soup.find('p', class_='question-url')
        time.sleep(2)

        if title:
            title = title.text.strip()
        else:
            title = detail_soup.find('div', class_='content-post-title')
            time.sleep(4)
            title = title.text.split("|")[1].strip()
        if url:
            url = url.text.strip()

        print(f"----------------------当前题解 标题: {title}")
        print(f"----------------------当前题解 刷题地址: {url}")
        
        # 获取题解内容
        content_html = detail_soup.find('div', class_='nc-slate-editor-content').prettify()
        # 题解内容 转成 md格式
        markdown_code = html2text.html2text(content_html)
        
        if url:
            md_content = f"{title}\n{url}\n{markdown_code}"
        else:
            md_content = f"{title}\n{markdown_code}"
        
        # 保存文件
        filename = f"{title.replace(' ', '_')}.md"
        with open(f"{MD_FILE_DIR}/{filename}", 'w', encoding='utf-8') as f:
            f.write(md_content)
        print(f"----------------------当前题解 已保存: {filename}----------------------\n")
        time.sleep(2)

if __name__ == '__main__':
    fetch_solutions()


```