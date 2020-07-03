测试 
## RejectCode

**Reject消息里的RejectCode字段值及其意义**

| 序号 | 字段名                | 值   | 意义                                       | SPV使用 | 日期     |
| ---- | --------------------- | ---- | ------------------------------------------ | ------- | -------- |
| 1    | RejectMalformed       | 0x01 | 消息格式不正确                             | 是      | 2020.7.3 |
| 2    | RejectInvalid         | 0x10 | 交易⾮法                         | 是      | 2020.7.3 |
| 3    | RejectObsolete        | 0x11 | 被协议拒绝的交易，协议版本太低                    | 否      | 2020.7.3 |
| 4    | RejectDuplicate       | 0x12 | 重复交易                                   | 是      | 2020.7.3 |
| 5    | RejectNonstandard     | 0x40 | 非标准消息                                 | 否        | 2020.7.3      |
| 6    | RejectDust            | 0x41 | 灰尘账户交易                               | 否      | 2020.7.3 |
| 7    | RejectInsufficientFee | 0x42 | 交易手续费检查不通过                       | 是        | 2020.7.3    |
| 8    | RejectCheckpoint      | 0x43 | 区块跟Checkpoint冲突，分叉checkpoint | 是        | 2020.7.3       |



## ErrCode

**Reject消息里Reason里json字符串包含的错误信息里的code字段及其意义**

| 序号 | 字段名                        | 值     | 意义                             | SPV使用 | 日期     |
| ---- | ----------------------------- | ------ | -------------------------------- | ------- | -------- |
| 1    | ErrFail                       | -1     | 失败                             | 否      | 2020.7.3 |
| 2    | ErrBlockFailure               | -10000 | 区块错误                         | 否      | 2020.7.3 |
| 3    | ErrBlockSerializeDeserialize  | -11000 | 区块序列化失败                   | 否      | 2020.7.3 |
| 4    | ErrBlockValidation            | -12000 | 区块合法性检查不通过             | 否      | 2020.7.3 |
| 5    | ErrBlockIneffectiveCoinbase   | -12001 | 区块中的Coinbase交易无效         | 否      | 2020.7.3 |
| 6    | ErrTxFailure                  | -20000 | 交易创建失败                     |         |          |
| 7    | ErrTxSerializeDeserialize     | -21000 | 交易序列化反序列化错误           |         |          |
| 8    | ErrTxValidation               | -22000 | 交易合法性检查不通过             |         |          |
| 9    | ErrTxInvalidInput             | -22001 | 交易input验证不通过              |         |          |
| 10   | ErrTxInvalidOutput            | -22002 | 交易output验证不通过             |         |          |
| 11   | ErrTxBalance                  | -22003 | 交易余额验证不通过               |         |          |
| 12   | ErrTxAttributeProgram         | -22004 | 交易Attribute验证不通过          |         |          |
| 13   | ErrTxSignature                | -22005 | 交易签名验证不通过               |         |          |
| 14   | ErrTxPayload                  | -22006 | 交易payload验证不通过            |         |          |
| 15   | ErrTxDoubleSpend              | -22007 | 交易双花检查验证不通过           |         |          |
| 16   | ErrTxSize                     | -22008 | 交易大小验证不通过               |         |          |
| 17   | ErrTxUnknownReferredTx        | -22009 | 交易前驱验证不通过               |         |          |
| 18   | ErrTxUTXOLocked               | -22010 | 交易含有UTXO处于锁定状态         |         |          |
| 19   | ErrTxDuplicate                | -22011 | 交易重复                         |         |          |
| 20   | ErrTxHeightVersion            | -22012 | 当前高度不支持此交易             |         |          |
| 21   | ErrTxAssetPrecision           | -22013 | 交易资产精度验证不通过           |         |          |
| 22   | ErrTxReturnDeposit            | -22014 | 取回质押金交易验证不通过         |         |          |
| 23   | ErrTxAppropriation            | -22015 | CR换届拨款交易验证不通过         |         |          |
| 24   | ErrTxAssetsRectify            | -22016 | CR总地址零钱换整交易验证不通过   |         |          |
| 25   | ErrTxRealWithdraw             | -22017 | 链上自动创建的提币交易验证不通过 |         |          |
| 26   | ErrTxSidechainValidation      | -23000 | 侧链挖矿交易验证不通过           |         |          |
| 27   | ErrTxSidechainDuplicate       | -23001 | 侧链挖矿交易重复                 |         |          |
| 28   | ErrTxSidechainPowConsensus    | -23002 | 侧链挖矿交易发起人不正确         |         |          |
| 29   | ErrDPoSFailure                | -30000 | DPOS相关错误                     |         |          |
| 30   | ErrCRFailure                  | -40000 | CR相关错误                       |         |          |
| 31   | ErrDbFailure                  | -50000 | 数据库相关错误                   | 否       | 2020.7.3 |
| 32   | ErrP2pFailure                 | -60000 | P2P相关错误                      |         |          |
| 33   | ErrP2pReject                  | -61000 | 被P2P拒绝错误                    |         |          |
| 34   | ErrP2pRejectMalformed         | -61001 | 非网络引起的消息读取失败错误     |         |          |
| 35   | ErrP2pRejectInvalid           | -61002 | 消息的合法性检查不通过被拒       |         |          |
| 36   | ErrP2pRejectObsolete          | -61003 | 消息于协议不符被拒               |         |          |
| 37   | ErrP2pRejectDuplicate         | -61004 | 消息重复被拒                     |         |          |
| 38   | ErrP2pRejectNonstandard       | -61005 | 非标准消息被拒                   |         |          |
| 39   | ErrP2pRejectDust              | -61006 | 灰尘账户消息被拒                 |         |          |
| 40   | ErrP2pRejectInsufficientFee   | -61007 | 交易fee不足被拒                  |         |          |
| 41   | ErrP2pRejectCheckpoint        | -61008 | 消息在当前高度不支持被拒         |         |          |
| 42   | ErrPoolFailure                | -70000 | 区块池或者交易池验证不通过       |         |          |
| 43   | ErrTxPoolFailure              | -71000 | 交易池验证不通过                 |         |          |
| 44   | ErrTxPoolOverCapacity         | -71001 | 交易池超过最大限定值             |         |          |
| 45   | ErrTxPoolSidechainTxDuplicate | -71002 | 交易池里存在相同的侧链挖矿交易   |         |          |
| 46   | ErrTxPoolDPoSTxDuplicate      | -71003 | 交易池DPOS相关交易重复           |         |          |
| 47   | ErrTxPoolCRTxDuplicate        | -71004 | 交易池CR相关交易重复             |         |          |
| 48   | ErrTxPoolDoubleSpend          | -71005 | 交易池双花检查不通过             |         |          |
| 49   | ErrTxPoolTypeCastFailure      | -71006 | 交易池类型转换失败               |         |          |
| 50   | ErrTxPoolTxDuplicate          | -71007 | 交易池交易重复                   |         |          |


