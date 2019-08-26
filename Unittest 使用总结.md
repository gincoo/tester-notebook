# Unittest - Python 使用总结

## 批量执行

### 一、UnitTest TestSuite 控制用例执行的顺序

**UnitTest 框架默认 main() 方法执行，根据 ASCII 码的顺序加载测试用例，数字与字母的顺序为：0~9，A~Z,a~z** 
如果要让某个测试用例先执行，不能使用默认的 main() 方法，需要通过 **TestSuite 类的 addTest()** 方法按照一定的顺序来加载。

**示例**:

```python
class TestCase01(unittest.TestCase):

    def setUp(self):
        print("case开始执行")

    def tearDown(self):
        print("case结束执行")

    @classmethod
    def setUpClass(cls):
        print("case类开始执行")

    @classmethod
    def tearDownClass(cls):
        pass

    @unittest.skip("这个case不像执行")
    def test_07(self):
        print("执行case07")
        flag = "adfadfadfadfadsfaqeewr"
        s = "fads"
        self.assertIn(s, flag, msg="不包含")

    @unittest.skip("这个case不像执行")
    def test_01(self):
        TestCase01.a = 5
        print("执行case01")
        # res = requests.get(url=url,params=data).json()
        data1 = {
            "user": "11111"
        }
        self.assertDictEqual(data1, data)

    @unittest.skip("这个case不像执行")
    def test_02(self):
        print("----------------> 执行case02")
        data1 = {
            "username": "1111",
            "password": "22222"
        }
        self.assertDictEqual(data1, data, msg="这两个字典不相等")
	
    @unittest.skip("这个case不像执行")
    def test_03(self):
        print("执行case03")
        flag = True
        self.assertFalse(flag, msg="不等于True")

    @unittest.skip("这个case不像执行")
    def test_04(self):
        print("执行case04")
        flag = False
        self.assertTrue(flag, msg="不等于False")

    @unittest.skipIf(host != "http://www.imooc.com", "这个case不执行")
    def test_05(self):
        print("执行case05")
        flag = "111"
        flag1 = "2222"
        self.assertEqual(flag, flag1, msg="两个str不相等")

    def test_06(self):
        res = request.run_main('get', url, data)
        print(res)


if __name__ == "__main__":
    suite = unittest.TestSuite()
    '''
    # TestSuite 控制执行顺序
    suite.addTest(TestCase01('test_06'))
    suite.addTest(TestCase01('test_04'))
    suite.addTest(TestCase01('test_02'))
    suite.addTest(TestCase01('test_05'))
    suite.addTest(TestCase01('test_01'))
    suite.addTest(TestCase01('test_07'))
    runner = unittest.TextTestRunner()
    runner.run(suite)
    '''
    # TestSuite 另一种写法
    tests = [TestCase01('test_06'), TestCase01('test_02'), TestCase01('test_03'), TestCase01('test_05'),
             TestCase01('test_01')]
    suite.addTests(tests)#
    runner = unittest.TextTestRunner()
    runner.run(suite)
```

### 二、 使用 UnitTest TestLoader类 discover() 函数执行更多测试用例

Python Unittest discover() 方法与执行顺序补充

可以根据不同的功能创建不同的测试文件，甚至是不同的测试目录，测试文件中还可以将不同的小功能划分为不同的测试类，在类下编写测试用例，让整体结构更加清晰

但通过addTest()添加、删除测试用例就变得非常麻烦

TestLoader 类中提供的 discover() 方法可以自动识别测试用例.py文件。

```python
discover(start_dir,pattern='test*.py',top_level_dir= None)
```

找到指定目录下所有测试模块，并可递归查到子目录下的测试模块，只有匹配到文件名时才加载

- start_dir：要测试的模块名或测试用例目录

- pattern='test\*.py'：表示用例文件名的匹配原则。此处匹配以“test”开头的.py 类型的文件，* 表示任意多个字符


- top_level_dir= None 测试模块的顶层目录，如果没有顶层目录，默认为None


**实例1：**

```python
import unittest
test_dir = './'
#定义测试目录为当前目录
discover = unittest.defaultTestLoader.discover(test_dir,pattern='test*.py')
if __name__ == '__main__':
	runner = unittest.TextTestRunner()
	runner.run(discover)
```

discover（）方法会自动根据测试目录 test_dir 匹配查找测试用例文件，并将查找到的测试用例组装到测试套件中，因此，可以直接通过
run()方法执行 discover，大大简化了测试用例的查找与执行

**实例2：**

```python
suite = unittest.TestSuite()
all_cases = unittest.defaultTestLoader.discover(PY_PATH,'Test*.py')
#discover()方法会自动根据测试目录匹配查找测试用例文件（Test*.py）,并将查找到的测试用例组装到测试套件中
[suite.addTests(case) for case in all_cases]
report_html = BeautifulReport.BeautifulReport(suite)
```

