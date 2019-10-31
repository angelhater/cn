# 访问管理实践
### 访问管理概述

访问控制（Identity and Access Management， IAM）是京东云提供的一项用户身份管理与资源访问控制服务。
IAM Policy是基于用户的授权策略。通过设置 IAM Policy，您可以集中管理您的用户（比如员工、系统或应用程序），
以及控制用户可以访问您名下哪些资源的权限。比如能够限制您的用户只拥有对某一个 Bucket 的读权限。
子账号是从属于主账号的，并且这些账号不能拥有任何实际资源，所有资源都属于主账号。

### 访问管理功能

- 主账号资源的授权
可以将主账号的资源授权给其他人员，包括子账号或者是其它主账号，而不需要分享主账号相关的身份凭证(AK/SK)。
- 主账号安全
可以通过授予与主账号相同的对于OSS的系统管理员权限（JDCloudOSSAdmin），保证主账号安全。
- 精细化的权限管理
可以针对不同的资源为不同的人员授予不同的访问权限。例如，可以允许某些子账号拥有某个 OSS 存储空间的读权限，而另外一些子账号或者其他京东云主账号
可以拥有某个 OSS 存储空间中对象的写权限等。

### 访问管理应用场景

#### 企业子账号权限管理

企业内不同岗位的员工需要拥有该企业云资源的最小化访问权限。

场景：某个企业拥有很多京东云资源，包括 VPC 实例、 CDN 实例、 OSS 存储空间和对象等。该企业同时拥有很多员工，包括开发人员、测试人员、运维人员等。
部分开发人员需要拥有其所在项目相关的开发机云资源的读写权限，测试人员需要拥有其所在项目的测试机云资源的读写权限，运维人员负责机器的购买和日常运营。
当企业员工人员变动、职责或参与项目发生变更，应将修改对应的权限，做好权限最小化管理。

####  不同企业之间的权限管理

不同企业间由于业务合作需要进行云资源的共享。

场景：某企业由于业务合作需要将云资源与其他企业分享，或者某企业拥有很多云资源时，该企业希望能专注产品研发，而将云资源运维工作授权给其他运营企业来实
施。当合作终止时，收回对应的管理权限。


访问管理策略语法
策略（policy）由若干元素构成，用来描述授权的具体信息。核心元素包括委托人（principal）、操作（action）、资源（resource）、
生效条件（condition）以及效力（effect）。如需了解更多，请查看[基于IAM Policy的权限控制](../../Operation-Guide/Access-Control/Access-Control-Base-On-IAM-Policy.md)。

IAM Policy示例

该样例描述为：允许属于主账号 ID 1234567890098 下的子账号 user1，拥有对OSS存储桶 bucketA与 bucketB下的前缀为test/对象读写对象的权限，以及消息队列（JCQ）管理员权限。
```
{
	"Statement": [{
		"Action": [
			"oss:PutObject",
			"oss:GetObject"
		],
		"Effect": "Allow",
		"Resource": [
			"jrn:oss:::bucketA/test/*",
			"jrn:oss:::bucketB/test/*"
		]
	}, {
		"Action": [
			"jcq:*"
		],
		"Effect": "Allow",
		"Resource": [
			"*"
		]
	}],
	"Version": "3"
}
```





