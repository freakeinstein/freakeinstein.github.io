---
layout: post
title: Programming in lua [ tutorial ] - ( quick reference ).
---

This quick reference that I've created, is based on the book `programming in lua - 3rd edition` [link](https://www.lua.org/pil/).


```lua
-- based on lua text book --
```


```lua
print("hello world")

```




    hello world	





```lua
function fact(n)
    if n == 1 then return 1 end
    return n*fact(n-1)
end

print(fact(3))
```




    6	





```lua
2^3
```




    8	





```lua
print(x)
```




    nil	





```lua
if nil then print("nil true") else print("nil is false") end
if false then print("false true") else print("false is false") end
if 0 then print("0 is true") end
if "" then print("empty string is true") end
if 2 then print("any digit is true") end
if "jubin" then print("any string is true") end
```




    nil is false	
    false is false	
    0 is true	
    empty string is true	
    any digit is true	
    any string is true	





```lua
str = "jubin\ajose jbn"
print(str)
print(#str)
```




    jubinjose jbn	
    14	





```lua
str = [==[
jubin jose
a = b[c[i]] -- equal signs given above to save this equation's double brackets ]]
cheruvallikattu
cmc 28
cherthala
]==]

print(str)
```




    jubin jose
    a = b[c[i]] -- equal signs given above to save this equation's double brackets ]]
    cheruvallikattu
    cmc 28
    cherthala
    	





```lua
print("-- lua automatically converts number to string where a string is expected and vice versa -- but good practie is to use tostring() and tonumber()")
```




    -- lua automatically converts number to string where a string is expected and vice versa -- but good practie is to use tostring() and tonumber()	





```lua
b = {}
b['name'] = 10
print(b.name) -- either way of access, 'cause everything is an entry in a table --
```




    10	





```lua
-- excersise 2.1 --
print(type(nil) == nil)
```




    false	
    





```lua
-- Modulo operator text: chapter 3--
print("10 % 3 = ",10%3)
print("10.13 % 3 = ",10.13%3)
print("10.13 % 1 = ",10.13%1)
print("10.13 - 10.13 % 1 = ",10.13-10.13%1)
print("10.1398765 - 10.1398765 % 0.01 = ",10.1398765-10.1398765%0.01)
```




    10 % 3 = 	1	
    10.13 % 3 = 	1.13	
    10.13 % 1 = 	0.13	
    10.13 - 10.13 % 1 = 	10	
    10.1398765 - 10.1398765 % 0.01 = 	10.13	





```lua
-- refer text chapter 3 portion 3.4 & 3.6 --
print(10 .. 6 == '106')
```




    true	
    





```lua
-- Table constructors => {} portion 3.7 --
days = {'sunday','monday','tuesday'}
print(days[2])

a = {x = 10, y = 20, jubin = 'jose', another = { inner = 10, deeper = 20, depth = 'zoo' }}
print(a[x],a.y,a.jubin, a.another.inner, a.another['deeper'], a['another'].depth)

a[-10] = -10
print(a[-10])
-- print(a.-10) -- will result in error --

-- a[+] = 'plus' -- will cause error --
a['+'] = 'plus' print(a['+']) -- is better way --

--[[ to free last element overheads during automatic
table generations, trailing comma is not a problem ]]--
z = {10, 2, 49, 31, 62,} for i=1,#z do print(z[i]) end
```




    monday	
    nil	20	jose	10	20	zoo	
    -10	
    plus	
    10	
    2	
    49	
    31	
    62	





```lua
-- chapter 4 assignment --
--[[ in lua, assignment => changing value of a table entry ]]--
x,y = 10,20
x,y = y,x -- no temp needed, lua does it :) --
print(x,y)
x,y,z = 0 -- is a mistake (not error) it just ignores y & z --
print(x,y,z)
```




    20	10	
    0	nil	nil	





```lua
-- local variable is local to a code block or local to a """chunk""" of code --
-- in interactive mode, a chunk is a set of lines before hitting enter --
-- to eliminate this problem, use do - end --
local outlier = 10
do  -- works in terminal only
    local inside_do = 10
end
print(outlier,inside_do)

-- just like other languages code blocks like for, while --
-- local behaves locally within that block --
```




    10	nil	





```lua
for var = 1,2,0.5 do
    print(var)
end
--[[ important notes:
1. for loop evaluates all three conditions once before loop starts
2. var is local variable  ]]--
```




    1	
    1.5	
    2	





```lua
--[[  generic for loop traverses all values returned by an iterator function ]]--
for k,v in pairs(a)
do 
    print(k,v)
end -- we could write our own iterative function like pairs() --
```




    jubin	jose	
    +	plus	
    -10	-10	
    x	10	
    y	20	
    another	{
      deeper : 20
      depth : zoo
      inner : 10
    }




** upcoming five chunks related to function calls **


```lua
-- functions --
-- if a function has only singlle argument, no need for paranthesis --
print 'jubin'
-- print os.date() -- will show error actual call: below --
print(os.date())

-- object oriented call to function --
-- x:function(y) -- => function(x,y)

-- no. of arguments may vary while calling a function --
function foo(a,b,c)
    print(a,b,c)
end
foo(1,2)
foo(1,2,3,4)

-- default function arguments --
function foo1(n)
    n = n or 17 -- 1 is default value --
    print(n)
end
foo1()
foo1(71)

-- function returns multiple results --
function foo2(n)
    return n,n^2,'jubin'
end
print(foo2(2))
```




    jubin	
    Wed Jun 29 21:23:02 2016	
    1	2	nil	
    1	2	3	
    17	
    71	
    2	4	jubin	





```lua
-- some other points to note when function call in list --
-- pre requisits --
function ff0() end
function ff1() return 'a' end
function ff2() return 'a','b' end
-- situations: --
-- 1) only function call in a list OR function call at the end --
-- it produces all results if any --
x,y = ff0() print(x,y)
x,y = ff1() print(x,y)
x = ff2() print(x)
x,y,z = 10,ff2() print(x,y,z)
print(type(foo2(2))) -- special case --
-- 2) A function call that is not the last element in the list --
-- always produces exactly one result --
x,y = ff2(),20 print(x,y)
x,y,z = ff2(),20 print(x,y,z)
x,y,z = ff0(),20,30 print(x,y,z)
print(type(foo2(2)),10) -- special case --
-- 3) function call in an expression it behave as (2) --
x = ff2() .. ' man' print(x)
x = foo2(2)+1 print(x)
```




    nil	nil	
    a	nil	
    a	
    10	a	b	
    number	
    a	20	
    a	20	nil	
    nil	20	30	
    number	10	
    a man	
    3	





```lua
-- 4) a constructer works in the similar way as well --
t = {ff2()} print(t)
t = {10,ff2()} print(t)
t = {ff2(),10} print(t)
```




    {
      1 : a
      2 : b
    }
    {
      1 : 10
      2 : a
      3 : b
    }
    {
      1 : a
      2 : 10
    }





```lua
-- 5) return values --
function returner(i)
    if i == 0 then return ff0()
    elseif i == 1 then return ff1()
    elseif i == 2 then return ff2()
    elseif i == 3 then return (ff2()) -- a paranthesis changes result -- 
    end
end

print(returner(2))
print(returner(3))

-- a special function that returns multiple values --
print(table.unpack{1,2,3})
```




    a	b	
    a	
    1	2	3	





```lua
-- veriadic functions --
-- functions can have any no of arguments into a single array --
function foo(...)
    print(...) -- these 3 dots are parameters 'vararg expression' --
    local sum = 0
    for i in ipairs{...} do
        sum = sum + i
    end
    print(sum)
end
a = {1,2,3,4,5,6,}
foo(table.unpack(a))

-- function with named parameters --
-- instead of passing a lot of parameters and having --
-- confusion about the parameter positions of the functions --
-- we could use the technique of a table to name parameters --
function swap(arg)
    return arg.right,arg.left
end
sl,sr = swap{left = 10,right = 20}
print(sl,sr)
```




    1	2	3	4	5	6	
    21	
    20	10	




** More on functions ** chapter 6


```lua
--[[ 1. functions are first class values => ike variables 
     2. they have lexical scope => they can access variables of their enclosing functions
        (inspired by functional programmng) ]]--
-- functions are anonymouse; they dont have name, what we use is a variable name that adress thaat function --
a = { p=print } a.p('jubin jose')
print = math.sin a.p(print(1))
```




    jubin jose	
    0.8414709848079	





```lua
-- restart kernal here !! (problems with print()) --
-- two ways of writing functions --
-- 1 -- 
function fun()
    print('jubin')
end
-- 2 --
fun1 = function()
    print('jose')
end
fun();fun1()
```




    jubin	
    jose	





```lua
--[[ higher order functions (function that gets another function as an argument) 
and returning anonymous functions ]]--
function derivative (f,delta) -- f is a function which is given into for computation, --
                                -- just like we do in sort(list,f) method, --
                                -- f determines which one is should go to top in two values --
    delta = delta or 1e-4 -- setting default param value --
    return function(x)
        return (f(x+delta) - f(x))/delta
        end
end

c = derivative(math.sin)
print(math.cos(5.2),c(5.2)) -- derivative of sin is cos, it must give approx. same value --

```




    0.46851667130038	0.46856084325086	





```lua
-- closures just works like objects--
function newCounter()
    local i = 0
    return function ()
        i = i + 1
        return i
    end
end
c1 = newCounter()
print('c1',c1())
print('c1',c1())
c2 = newCounter()
print('c2',c2())
print('c1',c1())
print('c2',c2())
```




    c1	1	
    c1	2	
    c2	1	
    c1	3	
    c2	2	




**Iterators and Generic for** chapter 7 (will be updated soon)


```lua

```
