blocks 代码块
1.
def hello 
    puts 'hello method start'
    yield
    yield #会执行调用的代码快
    puts 'hello method end'
end

hello {puts 'i am in block'}

会执行两次i am in block 
2.
def hello 
    puts 'hello method start'
    yield('hello','world')
    puts 'hello method end'
end

hello {|x,y| puts "i am in block ,#{x} #{y}"}

3.
def hello name
    puts 'hello method start'
    
    result = "hello" + name 
    yield(result)

    puts 'hello method end'
end

hello('world'){|x| puts "i am in block ,i got #{x}"}

4.
['cat','dog','frog'].each do |animal|
    puts animal
end

puts '-'*30
['cat','dog','frog'].each{|animal| puts animal}



5.
10.times do |t|
  puts t 
end

puts '-'*30
('a'..'d').each {|char| puts char}	


6. #代码快的作用域的问题 在ruby2.0被解决现在代码块不会被外部变量名字污染
x = 1

[1,2,3].each {|x| puts x}

puts x 

#在代码块内部声明的局部变量 不会被外部变量访问到的 但是内部变量可以访问外部变量

7.
sum = 0 

[1,2,3].each {|x|  sum += x}

puts sum
#内部变量可以修改外部变量 


8.#代码快可以有返回值的
class Array
  def find
    each do |value|
      return value if yield(value)
    end
    nil
  end
end

puts [1,2,3].find {|x| x==2}


9 #代码块可以做命名参数 可以更显示的让别人知道需要代码快 代码快可以向其他方法传递  向其他方法再次传递 yeild传递结果 这种可以除了结果意外的东西
def hello name,&block  # 逻辑与表明需要的代码快
  puts "hello #{name},from method"
  block.call(name)    #用call 向外部表明需要的变量
end

hello('434'){|x| puts "hello #{x} from block"}

10. #关键字block_given 可以判断函数是否调用代码块
def hello
  if block_given?
    yield
  else
    puts "hello from method"
  end
end

hello

puts'-'*30

hello {puts 'hello from block'}

11.#代码块 可以用来作为一个closure闭包 代码块作用域是绑定上下的作用域
#一般少用 ...
def counter
  sum = 0
  proc{|x| x = 1 unless x; sum +=x}
end

c2 = counter
puts c2.call(1)
puts c2.call(2)
puts c2.call(3)


12. 代码快的创建  在方法创建的时候 匿名代码快 命名的代码快lambda proc
hello = -> (name){"hello #{name}"} 代码块的定义
puts hello.call('343')

puts '-' *30

hello3 =lambda {|name| "hello #{name}"}
puts hello3.call('343')

puts '-'*30

hello2 = proc {|name| "hello #{name}"}
puts hello2.call
puts hello2.call('343')



lambda和proc的区别
1.参数的不同
lambda会检查参数的多跟少 参数多或者少了都会报 augmentError会检测自己的参数
proc不会检查参数的多跟少 少了就补上nil 多了就舍弃多余的参数会调整自己的参数

2.return的作用域不同
lambda 使用return 会把结果返回给使用lanmda的对象
proce会返回给作用域 定义proc的作用域

ruby中的Exception
ruby all Exception inherited from Exception Class

常见的Exception 
StandardError
SyntasError
RuntimeError
ArgumentError
NameError
etc.

Exception 抓取
#ruby中的关键字raise主动抛出异常
def hello name
  raise name
end

hello # => ArugmentError 没有传递参数报异常

hello('343')# => RuntimeError 有传递参数  用raise抛出的异常都是runtimeError


def hello
  raise
end


begin
  hello
rescue RuntimeError
  puts 'got it'
end




#exception catch

begin
  hello
rescue => e
  puts "catch exception with name: #{e.class}"
else
  #..如果没有发生异常处理逻辑
ensure
  # ensure 无论代码发生什么 这个逻辑一定执行
end


#变量交换 ruby中可以用一个等号让多个变量完成赋值
a = 1
b = 2
b, a = a, b
puts a
puts b

puts '-' *30
#会依次赋值
x = [1,2,3]
a,b = x
puts a
puts b

puts '-'*30
#*b会接受剩下的参数
x =[1,2,3]
a, *b = x
puts a
p b


#number 
puts 1/10
puts 1/10.0
puts '-' *30



#String  字符串可以用百分号%加Q  等同于“”  %加q等同于 ‘’

a ="world"
b = %Q{
    hello
    #{a}
}
puts b

puts '-' *30
# <<-HERE开始 到HERE结束
a = <<-HERE
hello world
#{b}
HERE
puts a 



#array 用百分号%w定义数组 每个元素都是字符串

a = %w[a b c 1]
p a




