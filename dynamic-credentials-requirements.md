# 动态证书需求
## 需求来源
国哥：身份的使用才是加分项，我们需要一个感动人心的Demo来演示身份动态证明的使用场景。

## 场景概述
场景改编自 Hyperledger-Indy 的 getting-started 中 Alice 的求职故事。我们延用 Alice 的故事，并稍加修改来构思探索。Alice 是虚构的 Faber 学院的毕业生，想要在虚构公司 Acme Corp. 申请工作。她一有工作就想向 Thrift Bank 申请贷款，以便她可以买车。她想用她的大学成绩单来证明她在求职申请上的学历，并且一旦聘用，艾丽丝想用在公司提供的`收入证明 > M`作为她贷款信用的证据。

## 场景分析
1. 这是一个定制化场景
1. 相关用户：Alice 、 Faber College 、 Acme Corp 、 Thrift Bank
1. 交互：Alice -> Faber 毕业证书申请表 、Faber -> Alice 毕业证书 、 Acme -> Alice 收入证明
1. 用户界面：Alice = App 、 Faber / Acme / Thrift = Server

## 界面增加
### App 界面
#### App - 联系人
1. Alice 能够通过输入 Proxy Address 添加 Faber / Acme / Thrift (F.A.T) 作为联系人。
	- Get F.A.T's Profiles
1. Alice 能接收来自联系人的证明文件，也能够向联系人发送授权信息。
	- F.A.T's URL for Query
	- F.A.T's URL for Send

### Server (F.A.T)
#### Server - Frontend
1. Faber 管理员能够读取到 Alice 的证书申请，并决定是否签名颁发。
	- Alice 的申请内容可能包含：毕业证书申请表（根据 Faber 定义的证书申请表 Schema 填写）、Alice 的个人身份证明
	- Faber 管理员审批，生成证书签名后，等待 Alice 查询。在签发后2天时间内，Alice 可查询并下载证书。
	- Faber 证书上链，证书撤销：
		- ……
1. Acme 管理员能够读取到 Alice 的毕业证书文件，并开放 Alice 在职证明查询接口。
	- Acme 管理员读取 Alice 毕业证书文件，验证：是否由 Faber 签发？是否发给 Alice？是否在有效期内？是否撤销？
	- Acme 管理员审批，为 Alice 创建一个在职证明查询接口。在开放接口的3天内，得到 Alice 授权的人能够得到授权的问题对应的答案：`Alice的年收入 > M`: true/false。
1. Thrift 管理员能够接收 Alice 的授权文件，并向 Acme 提交授权文件，查询问题对应的答案。
	- Thrift 管理员能够读取 Alice 的授权文件
	- 将授权文件 Redirect 到 Acme 提供的查询接口，得到返回结果。

## Workflow 方块图

需要一个怎样的流程图?
