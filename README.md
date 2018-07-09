# export 和 import

export用于对外输出本模块（一个文件可以理解为一个模块）变量的接口

import用于在一个模块中加载另一个含有export接口的模块

// a.js
var sex = "man"
var echo = function (value) {
    console.log(value)
}
export {
	sex,
    echo
}
// 通过向大括号中添加sex，echo变量并且export输出，就可以将对应变量值以sex、echo变量标识符形式暴露给其他文件而被读取到
// 不能写成export sex这样的方式，如果这样就相当于export "boy",外部文件就获取不到该文件的内部变量sex的值，因为没有对外输出变量接口,只是输出的字符串

// b.js
// 通过import获取a.js文件的内部变量，{}括号内的变量来自于a.js文件export出的变量标识符
import {sex, echo} from "./a.js"
import * as utils from './a.js'
console.log(sex)
utils.echo(sex)
a.js文件也可以按如下export语法写，但不如上边直观，不太推荐。

// a.js
export var sex="boy";
export var echo=function(value){
　　console.log(value)
}

// 因为function echo(){}等价于 var echo=function(){}所以也可以写成
export function echo(value){
　　　console.log(value)
}

# export default 和 import

前面的例子可以看出，b.js使用import命令的时候，用户需要知道a.js所暴露出的变量标识符，否则无法加载。可以使用export default命令，为模块指定默认输出，这样就不需要知道所要加载模块的变量名。

// a.js
var sex="boy"
export default sex //（sex不能加大括号）
// 原本直接export sex外部是无法识别的，加上default就可以了.但是一个文件内最多只能有一个export default。
// 其实此处相当于为sex变量值"boy"起了一个系统默认的变量名default，自然default只能有一个值，所以一个文件内不能有多个export default。

// b.js
// 本质上，a.js文件的export default输出一个叫做default的变量，然后系统允许你为它取任意名字。所以可以为import的模块起任何变量名，且不需要用大括号包含
import any from "./a.js"
import any12 from "./a.js" 
console.log(any,any12)   // boy,boy

