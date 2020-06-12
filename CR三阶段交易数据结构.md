##CR三阶段交易数据结构

### 1.CR三阶段新增提案类型

#### 1.1提案选举秘书长

**交易类型： CRCProposal**

**proposalType：**SecretaryGeneral CRCProposalType = 0x0400

| Field                     | Type    | Usage                                                    |
| ------------------------- | ------- | -------------------------------------------------------- |
| ProposalType              | Uint16  | 提案类型                                                 |
| CategoryData              | String  | 类别数据                                                 |
| OwnerPublicKey            | []byte  | 提案所有者，也就是提案负责人                             |
| DraftHash                 | Uint256 | 提案原文hash                                             |
| SecretaryGeneralPublicKey | []byte  | 新秘书长公钥                                             |
| SecretaryGeneralDID       | Uint168 | 新秘书长DID                                              |
| Signature                 | []byte  | 提案发起者签名                                           |
| SecretaryGeneraSignature  | []byte  | 新秘书长签名(注意：新秘书长签名内容不包括提案发起人签名) |
| CRCouncilMemberDID        | Uint168 | 推荐人的DID                                              |
| CRCouncilMemberSignature  | []byte  | 推荐人签名                                               |



#### 1.2提案更换另外一个提案负责人

**交易类型： CRCProposal**

**proposalType：**ChangeProposalOwner CRCProposalType = 0x0401

| Field                    | Type    | Usage                                                  |
| ------------------------ | ------- | ------------------------------------------------------ |
| ProposalType             | Uint16  | 提案类型                                               |
| CategoryData             | String  | 类别数据                                               |
| OwnerPublicKey           | []byte  | 提案所有者，也就是提案负责人                           |
| DraftHash                | Uint256 | 提案原文hash                                           |
| TargetProposalHash       | Uint256 | 需要修改提案负责人的提案的hash                         |
| NewRecipient             | Uint168 | 新ELA接受地址                                          |
| NewOwnerPublicKey        | []byte  | 新提案负责人公钥                                       |
| Signature                | []byte  | 提案发起者签名                                         |
| NewOwnerSignature        | []byte  | 新提案负责人签名(注意：签名内容不包括提案发起人的签名) |
| CRCouncilMemberDID       | Uint168 | 推荐人的DID                                            |
| CRCouncilMemberSignature | []byte  | 推荐人签名                                             |



#### 1.3提案中止另外一个提案

**交易类型： CRCProposal**

**proposalType：**CloseProposal CRCProposalType = 0x0402

| Field                    | Type    | Usage                        |
| ------------------------ | ------- | ---------------------------- |
| ProposalType             | Uint16  | 提案类型                     |
| CategoryData             | String  | 类别数据                     |
| OwnerPublicKey           | []byte  | 提案所有者，也就是提案负责人 |
| DraftHash                | Uint256 | The hash of draft proposal.  |
| TargetProposalHash       | Uint256 | 需要终止的提案的hash         |
| Signature                | []byte  | 提案发起者签名               |
| CRCouncilMemberDID       | Uint168 | 推荐人的DID                  |
| CRCouncilMemberSignature | []byte  | 推荐人签名                   |



### 2.CR二阶段遗留问题处理

#### 2.1CR总地址零钱换整

**交易类型：CRAssetsRectify**

**payload结构为空**

要求inputs必须不小于720个，不大于1440

outputs只能是一个

且所有的inputs与outputs都是CRAssetsAddress对应的proposalhash

不需要签名



#### 2.2新CR提案取款交易

**交易类型：CRCProposalWithdraw**

**payloadVersion:** CRCProposalWithdrawVersion01 byte = 0x01

| 字段           | 类型    | 用途           |
| -------------- | ------- | -------------- |
| ProposalHash   | Uint256 | 提案Hash       |
| OwnerPublicKey | []byte  | 提案负责人公钥 |
| Recipient      | Uint168 | ELA接受地址    |
| Amount         | Fixed64 | 提款金额       |
| Signature      | []byte  | 提案负责人签名 |



#### 2.3链上自动生成提案取款交易

**交易类型：CRCProposalRealWithdraw**

| 字段                      | 类型      | 用途     |
| ------------------------- | --------- | -------- |
| WithdrawTransactionHashes | []Uint256 | 提案Hash |

需要提案取款交易与output一一对应

如果有找零，找零的output需要放在outputs的最后















