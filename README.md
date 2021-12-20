# 政务通——区块链助力政府办公

## 项目简介

​	区块链具有不可篡改性以及可追溯性，因此对于一些重要信息区块链更能够保障信息的安全。基于区块链的这两大特点，我们决定做一个基于区块链的政府办公小程序。可以在这款小程序上实现**协同办公**，**数据脱敏上链**，以及**数据溯源**打破数据孤岛等功能。以小程序为载体，体现了区块链在实际生活中的具体作用。总体设计分为五个模块。具体如下：

| 功能模块                                 | 技术特点                                                     |
| ---------------------------------------- | ------------------------------------------------------------ |
| 1. **用户管理模块**                      | 注册时候对用户信息进行**资产数字化处理**，用户密码等关键信息脱敏上链。存储的是通过sha256运算后的哈希值，保障了用户的安全。用户登录时，输入密码进行一次哈希运算，与链上比对，即完成“**确权**”，验证一致才可登陆。 |
| 2. **建言献策模块**                      | 用户留言内容记录上链，同时对留言内容**调用外部api**，如果留言内容涉及敏感词，则扣除用户信用积分。**打造一个好的社会信用生态** |
| **3巡检模块**                            | 用户打卡记录上链，涉及“数据溯源”                             |
| **4.政务合作模块**                       | 体现联盟链的**“多方协作”**特点，同时涉及到**“确权”。**       |
| **5.政府选择性开放数据以及数据追溯模块** | 政府选择性对特定用户公开指定信息，**打破数据孤岛**，同时对用户查看的信息进行追踪，实现**数据可追溯**，谁在什么时间查看了什么内容都将记录上链。 |

## 功能模块图及小程序体验图

- 功能模块图

- 小程序体验图

  

## 系统实现
1. ##### 注册登录：

   ##### 注册登录模块可使用户在区块链上生成一个账号，进而为用户提供设置数字指纹和确权登录的操作手段，以此实现用户的操作安全性，确保用户的账号数据安全为用户本人操作。

##### 1.1用户注册：注册即用户输入6-20位的字符串作为密码，然后在微信小程序端进行哈希值加密后再进行网络传输保存到云端服务器和区块链上，由于区块链具有公开透明性，因此对于用户的密码这些私密信息我们采用数据脱敏上链，用户密码通过sha256加密处理后，将密码哈希上链。如此一来保障了用户密码的安全。

- 小程序端界面展示图：

- 区块链端数据展示图：

##### 1.2.登录：确权登录的操作手段，以此实现用户的操作安全性，确保用户的账号数据安全为用户本人操作。用户密码后小程序端将做一次哈希运算。利用这个哈希值和区块链端链上这个用户id对应的密码哈希值比较，进行一次”确权“操作，校验一致后，通过则读取用户的信息展示到前端。读数据不会产生新的区块，因此区块链端没有新的信息产生：

小程序端界面图：

##### 2.建言献策：

​	我们模拟了普通用户可以在小程序上向政府提交一些意见，留言内容上链的同时会使用外部api对用户所发布的内容进行违规词检测，如果监测到违规词会将违规词用*符号替换，以保证软件内容文明友善。同时会对违规留言用户扣分，如果分数低于60分将无法留言。用户可输入建言标题和建言内容，确保内容无误后点击“提交建议”后数据将上传到云端服务器和区块链，在云端服务器中会调用api对用户所发布的内容进行违规词检测替换，若内容有不文明用词将扣除用户1点信用值，且将建言标题内容和信用扣除记录上传到区块链上，否则就只将建言标题内容上传到区块链上。

- 小程序界面展示图：

- 区块链端用户留言事件图：

- 区块链端用户违规留言事件图：

  

##### 3.建言浏览:

用户可在小程序首页浏览所有用户提交的建议，且每条建议会显示建议提交者ID、提交时间以及是否违规。

- 小程序端界面展示图:

##### 4.建言记录:

用户可在个人中心的信用值记录查看自己提交的建言的详细记录.

- 小程序界面图:

##### 5.巡检:

​	我们模拟了在实际生活中，政府部门经常会有一些任务，要求在什么时候去哪些地方巡查，也就涉及到用户打卡，我们将用户打卡记录上链。同时领导可以通过下属的用户ID查看他的打卡记录信息

- 小程序界面图:

- 区块链端界面图:

  

##### 6.政务合作

##### 6.1科员上传文件

​	政府要发布某一条消息往往不是某一个人决定的，而是多级领导审核后同意才会通过，在文件传输过程中，如何保障数据不被篡改，区块链就可以起到很大的作用。但是区块链存储数据对资源消耗特别大，因此我们决定对数据“轻装”上链。政府公文文件的pdf放链下本地数据库，文件的哈希值上链。需要验证的时候将pdf再做一次哈希运算与链上对比，一致则可以保证文件的未被篡改。

- 科员上传文件小程序界面图:

- 科员申请材料数据记录图

  

##### 6.2领导审核文件

​	科长和处长审核，提交意见以及签字照片，审核后意见以及签名照片哈希值上链。首先领导要校验文件是否未被篡改，将下载该文件进行一次哈希运算，通过文件ID去与链上该文件当初上链的哈希值做比对，保障文件没有被篡改过，保障安全性。两个领导审核流程是一样的，过程不上链，只将最后领导审核的意见，以及两个领导签字照片的哈希值上链。

- 科长审核界面图

- 处长审核界面图

- 领导签字照片哈希上链记录图

- 审核部门审核界面图

- 审核事件数据记录图

  

##### 6.3文件公示

通过审核的文件给所有人查看并下载，以及对用户下载进行追踪。将谁在什么时候下载了哪一份文件，以及文件下载次数这些信息记录上链。

- 浏览文件界面图

- 下载文件界面图

- 用户下载文件事件记录图

  

##### 7政府选择性开放数据以及数据追溯

政府人员选择性公开某些数据给特定人看并对谁在什么时间查看了进行追踪，记录上链。打破了数据孤岛，实现了数据的可追溯性。

- 政府选择性公开数据界面图

- 选择性公开信息事件记录图

  

数据追溯：用户查看了数据后，区块链端将会留有记录，谁在什么时间查阅了什么数据将会被记录到区块链日志中

- 用户查看数据界面图
- 用户查看数据事件图

## 开发者简介

## 开发者简介