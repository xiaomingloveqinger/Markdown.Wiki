###CR运营自己的DPOS节点方案

####CR委员认领DPOS节点，新增认领DPOS节点交易类型

- 实现方式：

  当选的CR委员可以在主链发起认领DPOS节点的交易，交易里明确指定当前运营的DPOS节点的PublicKey。交易验证通过后，该CR委员对应的DPOS节点领取成功，需要运行的节点包括ELA、Arbiter、以及各个侧链。

- 开发任务：

  1.添加CR委员认领DPOS节点的交易，支持DPOS节点认领；

  2.CR委员认领DPOS节点后DPOS共识直连网络建立根据新的CR委员；

  3.DPOS节点inactive需要扣除一定的金额；

  4.DPOS节点illegal后需要扣罚金（工作量大，如果开放illegal，以前的作恶证据需要开放，我记得之前链上因为代码问题导致有节点illegal了，专门改代码支持illegal的转为active，并关闭illegal的触发，这块要改动还需要测试illegal是否能正常工作，illegal证据有Proposal、VoteProposal、Block三种都要处理）；

  5.CR委员被弹劾，则CR委员的DPOS节点不再参与DPOS共识。

- 
  相关问题：

  是否要求PublicKey与CR委员注册的PublicKey一致？

  是否需要支持更新运营节点？

  CR委员被弹劾，则CR委员的DPOS节点不再参与DPOS共识，空缺的CR由谁来填补还是怎么处理？

  CR委员弹劾过多，触发临时选举，此时没有CR，那参与共识的CR有谁来代替还是怎么处理？

  

####Arbiter动态感知当前CR委员

- 实现方式：

  Arbiter通过RPC获取当前CR委员列表，并根据Arbiter的的publickey来判断哪些Arbiter参与跨链交易处理。开放给CR运营后，Arbiter节点要考虑到CR委员被弹劾后的情况。

- 开发任务：

  1.ELA之前的获取当前CR列表的rpc接口调整，支持获取最新CR列表；

  2.CR委员被弹劾，考虑CR委员维护的Arbiter节点会关机的情况；

- 相关问题：
  CR委员被弹劾，CR委员的Arbiter节点可能会因为CR委员没收益也不运行了，是CR委员被弹劾时Arbiter也不再能处理跨链交易么？(因为跨链验证需要时CR签名，如果CR弹劾了，Arbiter应该是不再处理跨链业务)，这样弹劾的CR越多，Arbiter处理跨链交易的稳定性越差，因为要签名的个数慢慢接近于全签名。

  CR委员因弹劾触发临时选举，此时由哪些Arbiter节点来处理跨链业务？



####侧链动态感知当前CR委员

- 实现方式：
  侧链需要通过SPV获取当前CR委员列表，SPV需要支持统计当前CR委员，并存入数据库，支持查询当前CR委员列表。同时开放CR要考虑到侧链作恶的情况。
- 开发任务：
  1. SPV支持统计CR委员列表，并支持持久化及查询；
  2. 调整侧链的验证逻辑，根据当前最新的CR委员进行SideAuxPow的共识验证；
  3. SPV支持按高度获取区块难度值；
  4. 在收到区块时，根据SPV获取当前高度难度值去验证主链区块头难度，要求难度一致以防止侧链节点作恶。

