# 1.Typescript开发环境的搭建

1. 下载并安装node环境
2. 安装typescript:npm i -g typescript
3. 创建一个ts文件
4. 使用tsc对ts进行文件进行编译

# 2.基本类型

1. 变量的类型声明:它是TS非常重要的一个特点,通过类型声明可以指定TS中变量(参数,形参)的类型,指定类型后,当为变量赋值时,ts编译器就会自动检查值是否符合类型声明,符合则赋值,否则报错,类型声明给变量设置了类型,使得变量只能存储某种类型的值

   ```
   //声明一个变量a,同时指定它的类型为number
   let a: number
   //a的类型设置为了number,以后也只能给它赋值为Number,设置成别的就会报错
   a = 10;
   a = 33;
   a = "hello"//报错
   
   //函数形参中的运用
   function sum(a: number, b: number):number {//规定函数的返回值为number
       return a + b
   }
   
   sum(123, '123','222')//形参b会报错,多传也会报错
   ```

2. 联合类型:可以使用|来连接多个类型

   ```
   let b: string | number
   b = 123
   b = 'hello'
   ```

3. any :表示的是任意类型,一个变量设置类型为any后相当于对该变量关闭了TS的类型检测(不建议使用)

   ```
   let b;隐式any(声明不赋值)
   let b: any(显示any)
   b = 1
   b = "123"
   b = true
   
   let s:string = b //此时不会报错,any可以赋值给任意变量,赋值给谁谁的类型检测就关闭了,所以不建议使用 
   ```

4. unknown:表示不确定类型的变量

   ```
   //unknown实际上就是一个类型安全的any,unknown类型的变量,不能直接赋值给其他变量
   let b:unknown
   b=123
   b='123'
   b=true
   b='789'
   let s:string
   s = b//此时会报错(此时b是字符串类型也会报错,希望不报错可以用下面的方法)
   
   //类型断言:可以用来告诉解析器变量的实际类型 
   //相当于对编译器说b就是字符串类型
   s = b as string//当b的类型是字符串时,运用类型断言,此时就不会报错了
   s = <string> b 此种写法也是类型断言,与上面一行效果一致
   
   //if判断
   if (typeof b === 'string') {//这样就不会报错
       s = b
   }
   ```

5. void:用来表示空,以函数为例,就表示没有返回值的函数

   ```
   function fn():void{
       return 123//此时就会报错,因为不能有不是表示空的值返回,null和undefined不会报错
   }
   ```

6. never:表示永远不会返回结果,连undefined和null都不会返回

   ```
   function fn():never{
       throw new Error('报错了!')
   }
   ```

7. 