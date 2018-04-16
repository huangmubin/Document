# 添加 UDID 发布测试版

1. 打开 developer.apple.com 网站
2. -> Account
3. -> Certificates, Identifiers & Profiles
4. -> Devices -> iPhone
5. -> Provisioning Profiles -> Distribution
6. 新增 +
7. 选择 iOS App Development -> Continue
8. 选择 App 的 id。
9. 选择开发者。
10. 选择手机。
11. 输入描述文件名字。
12. 下载后，双击下载下来的文件。
13. 打开要进行测试的 iOS 项目。
14. 在项目设置中的 Signing 取消 Automatically manage signing.
15. 然后在 Signing(Debug)  以及 Signing(Release) 中选择生成的描述文件。
16. 打包导出，并选择 Ad-hoc  方式

