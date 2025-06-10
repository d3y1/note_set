# Nowcoder export notes and convert to md files

导出全部笔记 转为md文件

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
# 获取的所有笔记id 保存目录
SOLUTION_ID_DIR = '/xxx/yyy/zzz/solutions'
# 获取的所有笔记id 文件名称
SOLUTION_IDS_FILE = 'all_solution_ids.txt'

def get_all_notes():
    session = requests.Session()
    session.headers.update({'Cookie': COOKIE})
    session.headers.update({
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
    })
    
    all_notes = []
    page = 1
    max_retry = 3
    
    # 每次获取一页 每页15个笔记
    while True:
        try:
            url = f"https://www.nowcoder.com/profile/{USER_ID}/note?noteType=0&query=&page={page}"
            print(f"----------------------当前页url: {url}\n")
            resp = session.get(url, timeout=10)
            resp.raise_for_status()
            print(f"----------------------当前页 10个笔记: {resp.text}\n")

            # json中获取10个笔记id
            soup = BeautifulSoup(resp.text, 'html.parser')
            note_links = [a['href'] for a in soup.select('.note-mod-bd.link-green')]
            print(f"----------------------当前页 10个笔记id: {note_links}\n")
            
            if not note_links:
                break

            all_notes.extend(note_links)
            print(f"----------------------第{page}页: 获取完成!\n")
            page += 1
            time.sleep(2)
            
        except Exception as e:
            print(f"----------------------ERROR: {e}\n")
            max_retry -= 1
            if max_retry <= 0:
                break
            time.sleep(5)


    # 从link中截取笔记id: ['/profile/11111111/note/detail/1155207?noteType=0','/profile/11111111/note/detail/1154827?noteType=0'] -> ['1155207', '1154827']
    # 方法1：字符串切片（需已知固定长度）
    # prefix_len = len('/profile/11111111/note/detail/')
    # all_note_ids = [link[prefix_len:-11] for link in all_notes]
    # 方法2：split分割（更灵活）
    all_note_ids = [link.split('/')[-1].split('?')[0] for link in all_notes]
    print(f"--------------------------all note ids: {all_note_ids}")

    # 创建保存目录
    os.makedirs(SOLUTION_ID_DIR, exist_ok=True)
    # 保存所有笔记id
    with open(f"{SOLUTION_ID_DIR}/{SOLUTION_IDS_FILE}", 'w', encoding='utf-8') as f:
        f.write(str(all_note_ids))

    return all_note_ids

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
    session.headers.update({
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
    })

    # 方法1 直接从API获取
    all_notes = get_all_notes()
    # 方法2 本地文件获取
    # all_notes = load_ids_from_txt(f"{SOLUTION_ID_DIR}/{SOLUTION_IDS_FILE}")
    print(f"----------------------所有笔记id: {all_notes}")

    time.sleep(2)
    
    # 创建md文件保存目录
    os.makedirs(MD_FILE_DIR, exist_ok=True)
    
    for solution in all_notes:
        print(f"----------------------当前笔记id: {solution}")

        # 抓取单篇笔记 示例: https://www.nowcoder.com/profile/11111111/note/detail/1155207?noteType=0
        solution_url = f'https://www.nowcoder.com/profile/{USER_ID}/note/detail/{solution}?noteType=0'
        print(f"----------------------当前笔记url: {solution_url}")
        detail_resp = session.get(solution_url, timeout=10)
        detail_resp.raise_for_status()
        detail_soup = BeautifulSoup(detail_resp.text, 'html.parser')
        
        time.sleep(2)

        # 提取内容（需适配牛客网实际HTML结构）
        # 获取笔记 标题
        title = detail_soup.find('h4', class_='notes-hd')
        time.sleep(3)

        if title:
            title = title.get_text().strip()

        print(f"----------------------当前笔记 标题: {title}")
        
        # 获取笔记代码内容
        content_html = detail_soup.find('div', class_='notes-bd').prettify()
        time.sleep(2)

        # 笔记代码内容 转成 md格式
        markdown_code = html2text.html2text(content_html)
        # 标题 + 代码
        md_content = f"{title}\n\n{markdown_code}"
        
        # 保存文件
        filename = f"{title.replace(' ', '_')}.md"
        with open(f"{MD_FILE_DIR}/{filename}", 'w', encoding='utf-8') as f:
            f.write(md_content)
        print(f"----------------------当前笔记 已保存: {filename}----------------------\n")
        time.sleep(2)

if __name__ == '__main__':
    fetch_solutions()


```