### CR三阶段参数调整

#### 1.参数新增

CRConfiguration里新增参数：

```go
// CR总地址零钱换整，单个交易所包括的UTXO最大个数
MaxCRAssetsAddressUTXOCount        uint32  `json:"MaxCRAssetsAddressUTXOCount"`

// CR总地址零钱换整，单个交易所包括的UTXO最小个数
MinCRAssetsAddressUTXOCount        uint32  `json:"MinCRAssetsAddressUTXOCount"`

// CR总地址零钱换整，起始高度
CRAssetsRectifyTransactionHeight   uint32  `json:"CRAssetsRectifyTransactionHeight"`

// CR总地址零钱换整，交易手续费
RectifyTxFee                       common.Fixed64 `json:"RectifyTxFee"`

// CR新提案取款交易，起始高度，此高度后只支持新提案取款交易，payloadVersion为0x01
CRCProposalWithdrawPayloadV1Height uint32  `json:"CRCProposalWithdrawPayloadV1Height"`

// CR新提案取款交易,链上自动创建的实际提款交易，包含N个钱包创建的交易，则手续费为 N * RectifyTxFee
RealWithdrawSingleFee              common.Fixed64 `json:"RealWithdrawSingleFee"`
```

配置文件参考：

```json
{
 	"Configuration": {
		 "CRConfiguration":{
  		 "MaxCRAssetsAddressUTXOCount":720,
 		   "MinCRAssetsAddressUTXOCount":1440,
  		 "CRAssetsRectifyTransactionHeight":21000,
  		 "CRCProposalWithdrawPayloadV1Height":22000,
  		 "RectifyTxFee":10000,
  		 "RealWithdrawSingleFee"：10000
 		 }
	}
}
```



#### 2.参数位置调整

以下五个参数从外层移动到CRConfiguration里，部分做了调整：

CRAssetsAddress    原来的CRCFoundation

CRExpensesAddress      原来的CRCommitteeAddress

CRCAddress

CRCommitteeStartHeight

CRVotingStartHeight

配置文件参考：

```json
{
 	"Configuration": {
		 "CRConfiguration":{
  		 "CRAssetsAddress":"",
 		   "CRExpensesAddress":"",
  		 "CRCAddress":"",
 		   "CRCommitteeStartHeight":1200,
  		 "CRVotingStartHeight":1000
 		 }
	}
}
```

