# WTF-NOTE

## 1. 数值类型
1. 布尔型
   `` bool public _bool = true;
2. 整型
   ``     // 整型
   ``     int public _int = -1; // 整数，包括负数
   ``     uint public _uint = 1; // 正整数
   ``     uint256 public _number = 20220330; // 256位正整数
3. 地址类型
   地址类型分为：
- 普通地址（address）: 存储一个 20 字节的值（以太坊地址的大小）。
- payable address: 比普通地址多了transfer和send两个成员方法，用于接收转账。
  ``     // 地址
  ``     address public _address = 0x7A58c0Be72BE218B41C608b7Fe7C5bB630736C71;
  ``     address payable public _address1 = payable(_address); // payable address，可以转账、查余额
  ``     // 地址类型的成员
  ``     uint256 public balance = _address1.balance; // balance of address
4. 定长字节数组
   字节数组bytes分两种:

定长: 属于数值类型，根据每个元素存储数据的大小分为 byte, bytes8, bytes32 等类型，每个元素最多存储 32 bytes数据。数组长度在声明之后不能改变。
不定长: 属于引用类型，数组长度在声明之后可以改变，包括 bytes 等
``     // 固定长度的字节数组
``     bytes32 public _byte32 = "MiniSolidity";
``     bytes1 public _byte = _byte32[0];
5.   枚举 enum
     枚举较为冷门，仅供了解
     ``     // 用enum将uint 0， 1， 2表示为Buy, Hold, Sell
     ``     enum ActionSet { Buy, Hold, Sell }
     ``     // 创建enum变量 action
     ``     ActionSet action = ActionSet.Buy;
     ``
## 2. 函数类型
### 函数的基本形式：
``  function <function name>(<parameter types>) {internal|external|public|private} [pure|view|payable] [returns (<return types>)]
方括号中的是可写可不写的关键字

### 函数可见性说明符
- public: 内部外部均可见。
- private: 只能从本合约内部访问，继承的合约也不能用。
- external: 只能从合约外部访问（但是可以用this.f()来调用，f是函数名）。
- internal: 只能从合约内部访问，继承的合约可以用。
  注意：
- 合约中定义的函数需明确指定可见性，它们没有默认值， 合约之外的函数，即"自由函数"，始终具有隐含internal可见性。
- public|private|internal 也可用于修饰状态变量。 public变量会自动生成同名的getter函数，用于查询数值。
- 没有标明可见性类型的状态变量，默认为internal。
### pure & view
pure : 不可读不可写
view： 可读不可写

### internal v.s. external
``     // internal: 内部
``     function minus() internal {
``         number = number - 1;
``     }
``
``     // 合约内的函数可以调用内部函数
``     function minusCall() external {
``         minus();
``     }
相当于给外部函数调用内部函数提供了一个接口

### payable
``     // payable: 递钱，能给合约支付eth的函数
``     function minusPayable() external payable returns(uint256 balance) {
``         minus();    
``         balance = address(this).balance;
``     }
``
（this关键字可以让我们引用合约地址)
我们可以在调用的时候写参数，就可以在调用函数的时候同时进行转账操作


