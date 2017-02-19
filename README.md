# How-to-learn-automationtesting-by-python
It is my learn how to  automation testing ,I hope,i can defeat myself!
 #!/usr/bin/python
 # -*- coding: UTF-8 -*-
 #前台自动发布产品脚本创建
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import Select
from selenium.common.exceptions import NoSuchElementException
from selenium.common.exceptions import NoAlertPresentException
import unittest, time, re
from _random import Random
from random import choice
from lib2to3.pgen2.driver import Driver

class Untitled(unittest.TestCase):
    def setUp(self):
        self.driver = webdriver.Firefox()
        self.driver.implicitly_wait(30)
        self.base_url = "http://test.huasuhui.com/"
        self.driver.maximize_window()
        self.verificationErrors = []
        self.accept_next_alert = True    
    def test_untitled(self):
        driver = self.driver
        driver.get(self.base_url + " ")
        driver.find_element_by_link_text(u"请登录").click() #登录操作
        driver.find_element_by_id("mobile").clear()
        driver.find_element_by_id("mobile").send_keys("13381735263")
        driver.find_element_by_id("password").clear()
        driver.find_element_by_id("password").send_keys("123456")
        driver.find_element_by_id("login").click()#点击登录button        
        driver.find_element_by_link_text(u"我的供求").click()#点击 我的供求
        
        cs=0
        jg=9000
        while cs < 5:            
            driver.find_element_by_link_text(u"单条发布").click()#点击 单条发布
            product_name=['product_name_group_0','product_name_group_1','product_name_group_2','product_name_group_3','product_name_group_4'] #将主要的产品写入数组中备用
            from random import choice#使用随机方法
            print choice(product_name)
            driver.implicitly_wait(3)
            driver.find_element_by_id(choice(product_name)).click()#将获取的随机值赋值到selenium对象
            item_no=['HQM','YF','GHX','WY','QML','XJL','G-2100','X110'] #牌号输入数组
            from random import choice
            print choice(item_no)
            driver.find_element_by_id('Trade_list_item_no').send_keys(choice(item_no))
            driver.implicitly_wait(3)
        #定义 用途 的对象
            usefunction=driver.find_element_by_id('Trade_list_usage')
            usefunction.click() #触发点击事件
            time.sleep(3)            
            functionno=['#Trade_list_usage > option:nth-child(1)','#Trade_list_usage > option:nth-child(2)','#Trade_list_usage > option:nth-child(3)','#Trade_list_usage > option:nth-child(4)','#Trade_list_usage > option:nth-child(5)',
                        '#Trade_list_usage > option:nth-child(6)','#Trade_list_usage > option:nth-child(7)','#Trade_list_usage > option:nth-child(8)','#Trade_list_usage > option:nth-child(9)','#Trade_list_usage > option:nth-child(10)']
            from random import choice
            print choice(functionno)
            driver.find_element_by_css_selector(choice(functionno)).click()#选择用途===》溶脂
            driver.implicitly_wait(3)
            price1=range(500,10000)
            from random import choice 
            print choice(price1)
            driver.find_element_by_id('Trade_list_price').send_keys(choice(price1))#输入价格
            driver.implicitly_wait(3)
            driver.find_element_by_id('Trade_list_quantity').send_keys('20')#输入数量
            driver.implicitly_wait(3)
            #随机选择仓库港口位置
            buffer_location=['#Trade_list_buffer_location > option:nth-child(1)','#Trade_list_buffer_location > option:nth-child(2)','#Trade_list_buffer_location > option:nth-child(3)','#Trade_list_buffer_location > option:nth-child(4)',
                             '#Trade_list_buffer_location > option:nth-child(5)','#Trade_list_buffer_location > option:nth-child(6)','#Trade_list_buffer_location > option:nth-child(7)','#Trade_list_buffer_location > option:nth-child(8)','#Trade_list_buffer_location > option:nth-child(9)',
                             '#Trade_list_buffer_location > option:nth-child(10)','#Trade_list_buffer_location > option:nth-child(11)']
            from random import choice
            print choice(buffer_location)
            driver.find_element_by_css_selector(choice(buffer_location)).click()
            driver.implicitly_wait(6)
            driver.find_element_by_id('Trade_list_delivery_date').send_keys('20')#输入交货时间
            driver.implicitly_wait(6)
            driver.find_element_by_id('Trade_list_validity').send_keys('30')#输入有效时间
            driver.implicitly_wait(6)
            driver.find_element_by_id('submit_create_product').click()#点击确认提交
            time.sleep(3)
            alert=driver.switch_to_alert()#处理页面弹出的警告，使用switch_to_alert()方法定位到alert/comfirm/prompt
            alert.accept()#使用test/accept/dismiss/send_keys按照需要进行操作 此处的accept是表示点击确认按钮
            driver.implicitly_wait(6)
            alert=driver.switch_to_alert()#处理第二个弹出的警告，原理同上
            alert.accept()
            time.sleep(3)
            cs=cs+1
            jg=jg-100
        time.sleep(3)
        driver.find_element_by_link_text('退出').click()
        time.sleep(6)
    
    def is_element_present(self, how, what):
        try: self.driver.find_element(by=how, value=what)
        except NoSuchElementException as e: return False
        return True
    
    def is_alert_present(self):
        try: self.driver.switch_to_alert()
        except NoAlertPresentException as e: return False
        return True
    
    def close_alert_and_get_its_text(self):
        try:
            alert = self.driver.switch_to_alert()
            alert_text = alert.text
            if self.accept_next_alert:
                alert.accept()
            else:
                alert.dismiss()
            return alert_text
        finally: self.accept_next_alert = True
    
    def tearDown(self):
        self.driver.close()
        self.assertEqual([], self.verificationErrors)

if __name__ == "__main__":
    unittest.main()
