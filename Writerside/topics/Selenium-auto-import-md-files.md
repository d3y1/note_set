# Selenium auto import md files

```Python

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.keys import Keys
import time

# 内容格式: ['牛客_魔法表.md','牛客_魔法阵.md','牛客_龙与地下城游戏问题.md']
MD_FILE_LIST = '/xxx/yyy/zzz/solution_titles_nc.txt'
# 本地md文件 实际存放路径
MD_FILE_REAL_DIR = '/xxx/yyy/zzz/solutions-ok-csdn'

# google chrome for testing & chromedriver 版本需要相同 比如: 137.0.7151.68 <- chrome://version/
# chrome & chromedriver download url: https://googlechromelabs.github.io/chrome-for-testing/
service = Service('/usr/local/bin/chromedriver')
driver = webdriver.Chrome(service=service)

print("----------------------------start----------------------------")
url = 'https://editor.csdn.net/md/?not_checkout=1&spm=1001.2101.3001.5352'
driver.get(f"{url}")
print(f"----------------------------edit url: {url}")

# 需要手动登录
time.sleep(15)

# csdn每日限制15篇
md_file_list = []
with open(f"{MD_FILE_LIST}", 'r') as file:
    # 读取并去除首尾空格
    content = file.read().strip()
    # 将字符串转为列表
    md_file_list = eval(content)

# 登录后 循环上传文件
for md_file in md_file_list:
    print(f"----------------------------md file: {md_file}")
    time.sleep(1)

    # 直接操作文件输入框 输入md文件 标题及内容
    file_input = driver.find_element(By.ID, "import-markdown-file-input")
    file_input.send_keys(f"{MD_FILE_REAL_DIR}/{md_file}")
    time.sleep(3)

    # 点击 '发布文章' 按钮
    driver.find_element(By.CSS_SELECTOR, ".btn.btn-publish").click()
    time.sleep(3)

    # 点击 '添加标签'按钮
    add_tag_btn = WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.CSS_SELECTOR, ".tag__btn-tag"))
    )
    add_tag_btn.click()

    # 搜索框输入 'java'标签
    search_input = driver.find_element(By.CSS_SELECTOR, ".el-input__inner")
    search_input.send_keys("java")
    time.sleep(1)
    # 按 'ENTER' 键
    search_input.send_keys(Keys.ENTER)

    # 等待标签添加完成（可选）
    WebDriverWait(driver, 5).until(
        EC.presence_of_element_located((By.CSS_SELECTOR, ".el-tag--light"))
    )

    # 点击 '关闭标签'弹出框
    close_btn = WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.CSS_SELECTOR, 
        ".mark_selection_box_body > .modal__close-button"))
    )
    if not close_btn.is_displayed():
        # 无视前端校验 直接javascript点击关闭
        driver.execute_script("arguments[0].click();", close_btn)
    else:
        close_btn.click()
    time.sleep(3)

    # 勾选 备份gitcode checkbox
    driver.find_element(By.CSS_SELECTOR, ".el-checkbox__input").click()
    time.sleep(2)

    # 点击 '发布'按钮 (最后步骤)
    driver.find_element(By.CSS_SELECTOR, ".button.btn-b-red.ml16").click()
    time.sleep(5)

    # 点击 '再写一篇'按钮
    new_btn = WebDriverWait(driver, 10).until(
        EC.element_to_be_clickable((By.CSS_SELECTOR, 
        ".success-modal-btn.active"))
    )
    # 无视 '选择身份'弹出框 直接点击 '再写一篇'按钮
    driver.execute_script("arguments[0].click();", new_btn)

    print(f"----------------------------md file: {md_file}发布成功!----------------------------\n")
    # 防止频率限制
    time.sleep(5)
driver.quit()

```