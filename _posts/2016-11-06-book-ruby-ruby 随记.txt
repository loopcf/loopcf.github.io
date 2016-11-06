ruby 代码规范
使用UTF-8编码
使用空格缩进，不使用tab, 1tab = 2spaces
不需要使用分号(;) 和反斜杆(\)链接代码

#等号的前后都要留一个空格
a = 1
b = "hello world"

#数组每个元素都用， 
c = ["pear","cat","dog"]

c2 = [  #每行两个空格
  "pear",
  "cat",
  "dog"
]

#hash的定义 建议 在hash大括号的开始和结束 都空格 在key和value都留一个空格
d = { name: "343", age: 18 }

d2 = { 
  name: "343",
  age: 18
}

#方法的定义和使用都不用加括号

def hello(name, age = 18)
  puts "hello #{name}, and age is #{age}"
end

def hello name ,age = 18
  puts "hello #{name}, and age is #{age}"
end

#2个空格和对齐






变量类型 
local variables 局部变量: a = 1,b = "hello"
constants 常量 Names=['john','alex']
global variables 全局变量 $platfrom = 'mac'
instance variables 实例变量 @name = "343"
class variables 类变量 @@counter = 20




#常量 
Name = '343'
Name = '3432' #=>output warning ruby中大写字母开头的是常量

Name.repalce '343_2' # => safe


#变量的scope
class User
  
  attr_reader :name

  @@counter = 0
 
  def initialize name
    @name = name
  
    @@counter +=1
  end

  def get_counter
    @@counter
  end

end

user = User.new '343'
puts user.name
puts user.get_counter

$$ 表示进程id pid
$: 表示 ruby loading path 加载路径


#Boolean表达式

&&,||,!
And,Or,Not





Instance Method & Instance Attribute
Instance Method 实例方法，成员方法，成员函数
Instance Attribute 实例变量，成员变量，属性 使用@定义

定义类 
class User

  def initialize name, age
    @name = name 
    @age = age
  end

  #getter
  def name
    @name
  end

  def age
    @age
  end

  #setter
  def name= name
    @name = name
  end

  def age= age
    @age = age
  end

end

user = User.new('hello', 18)
puts user.name
puts user.age

class User
  

  attr_reader :name
  attr_reader :age

  attr_writer :name
  attr_writer :age

  def initialize name,age
    @name = name
    @age = age
  end


end



attr_accessor :name #拥有reader跟wirter的效果



类方法和类变量

Class Method 类方法，静态方法
Class Variable 类变量 使用@@定义

类方法 self打头 或者是def类名.方法名

# class method & class variable

class User
  
  attr_accessor :name
  attr_accessor :age

  @@counter = 0

  def initialize name, age
    @name = name
    @age = age

    @@counter += 1
  end

  def say_hi
    puts "hello #{@name}, i am #{age}"
  end

  def self.get_counter
    @@counter
  end

end

puts User.get_counter
user = User.new('hello', 18)
puts User.get_counter



class_eval 和istance_eval

class_eval 
首先class_eval是只有类才能调用的，Class#class_eval Class类的实例方法
class_eval会重新打开当前类作用域


module Management

  def self.included base
    base.extend ClassMethods

    base.class_eval do
      setup_attribute
    end
  end

  module ClassMethods
    def setup_attribute
      puts 'setup_attribute'
    end
  end
end

class User
  include Management
end

#在注入模块的时候，自动调用某些方法

instance_eval 
instance_eval是所有类实例的方法
打开的是当前实例作用域
class User
end

User.class_eval do
  def hello
    'hello'
  end
end

User.instance_eval do
  def hi
    'hi'
  end
end

puts User.new.hello


method_missing
当前作用域上下文没有找到方法时就会调用method_missing方法


Module as a Namespace
可以在模块内部定义Module，Class，Constants
使用::来访问

module Management

  COMPANY_NAME = "343 Code Academy"

  module Track
    def track
      'track from Track module'
    end
  end

  class User
    def hello
      'hello from User class'
    end
  end

end

puts Management::COMPANY_NAME

puts '-' * 30
include Management::Track
puts track

puts '-' * 30
user = Management::User.new
puts user.hello


Gems ruby的包的管理工具 类似Linux的rpm deb
社区中Gem包涵了各个方面开发所需要的工具和组建
通过Gem命令来安装
gem 命令 
gem list #本地电脑安装了什么gem
gem install
gem uninstall
gem sources #gem安装的元服务器
有墙 切换国内淘宝镜像 https://ruby.taobao.org

require 和 load  #可以使用rb脚本文件
相同点是都会在$LOAD_PATH
require 调用文件的时候不需要后缀名 .rb
require 针对同样的文件只会调用一次 ,load会重复调用



$LOAD_PATH
Ruby代码的查找路径为当前的$LOAD_PATH环境变量
Ruby文件命名规则：文件的名字代表了当前的class/module的名字
