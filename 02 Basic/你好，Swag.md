# 你好，Sway

contract顶部的关键字定义了 Sway 中的四种程序类型之一。其他类型包括库、脚本和谓词。
// Sway 中编写的底层智能合约与 Solidity 中的合约没有什么不同
// 一些字节码部署了 API 和状态以与之交互
contract;

// ABI（应用程序二进制接口）明确定义了合约中存在的函数的签名
abi HelloModular {
    // “注释”存储表示函数的不纯操作
    // 在这种情况下，greet() 函数仅具有读取功能。
    // 注意：存储只能在合约类型程序中找到
    
    #[storage(read)]
    fn my_lucky_number() -> u64;
}

// Storage contains all of the state available in the contract 
storage {
    lucky_number: u64 = 777,
}

// The actual implementation of ABI for the contract
impl HelloModular for Contract {
    #[storage(read)]
    fn my_lucky_number() -> u64 {
        storage.lucky_number.read()
    }
}
