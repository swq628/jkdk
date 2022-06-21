# jkdk

## 郑州大学健康打卡自动脚本

---

### 使用必读

项目**时常更新**。如果你发现用该项目时原先能打上卡但是现在打不上卡了，可以看看项目是否更新没。一般会及时更新。

也就是说如果出现下图情况，在红框内有commits behind了，就需要点击右边的fetch upstream进行更新了。

![update](images/update.png)

---

### 目前发现打卡界面记录**IP地址**，不过仍能打卡成功，尚不清楚有何影响。请谨慎使用。

---

### 1. 注意：项目启用后60天无更新时，Actions功能会**自动关闭**，届时需要再次手动开启。

---

## 使用方法

1. 先把代码整个都clone下来，然后在此基础上自己创建一个github仓库，仓库设置为私人。或者把代码fork到你自己的仓库（不过这样改不了仓库的可见性为私人）

![fork截图](./images/fork.png)

2. 点击settings，找到Secrets

![settings](./images/settings.png)

3. 添加8个仓库密钥 username、password、province、city、position，分别表示学号、密码、省份、城市、具体位置、疫苗接种情况以及经度、纬度。如果想要使用微信通知打卡情况，步骤也在后面。

   

![添加仓库密钥](./images/secret.png)

   

![添加学号](./images/username.png)

   - 添加**学号**，name必须是username
   - **密码**的添加同理，但name必须是password
   - 添加**省份**，省份的name必须是province，value是参考

     https://gist.github.com/mayufo/4207ed3fa925e6b3df7559832af85165
     是所对应数字的前两位

   - **城市**的name必须是city，value是上面链接对应数字的第三、四位
   - **详细地址**就没有要求，但是name必须是position
   - **疫苗接种情况**：name是myvs_26，对应的是疫苗接种情况，具体填法如下(若无该项，则默认接种第二针)

        |  需填值 |含义              |
        |  ----  | ----            |
        |   1    | 已接种第1针       |
        |   2    | 已接种第2针       |
        |   3    | 尚未接种         |
        |   4    | 有禁忌症，无法接种 |
        |   5    | 已接种第3针      |
  - **经度**: name是jingdu，填入你所期望的位置的经度即可，可以在网上查找
  - **纬度**： name是weidu，如上同理。*
  - **微信通知**：name是key，
1. 扫描此微信二维码并关注微信公众号
[二维码](http://wxpusher.zjiecode.com/api/qrcode/hNHQXsGvGguORhwBHItWlaqUYvs79Ii59RpFN5YmuDIBOiO8YLQlqHd051TBfmeO.jpg)

2. 关注后在右下角”我的“这一栏中把UID替换到原先secrets中的微信key(**name是key，值即得到的uid**)中即可，除此之外，关注后会有消息通知uid的值。


4. 然后在左边的找到actions，选择enable action，这样就激活了action

![actions位置](./images/actions.png)

5. 结束。接下来会每日6点、6点10分和7点、7点10分自动打卡（多次打卡防止打卡失败）。不过这里**第一次**建议自己修改 .github/workflows 里面的 jkdk.yml 里的时间以进行一次打卡看看效果（有时候会因为网络问题打卡失败，不过因为设置了**多次打卡**的缘故，失败的几率会降低），注意修改为**UTC时间**，即比北京时间晚8个小时，具体可以参考有北京时间注释的那一行。

6. __**注意**__，如果GitHub action激活不了，则需要编辑一下.github/workflows 里面的 jkdk.yml文件，输入几个空格或者回车即可，然后提交，action就可以被激活。

7. 最终的结果
   ![actions结果](./images/result.png)

8. 每日打卡成功后的提醒
   <img src="./images/clock.png" alt="微信提醒" style="zoom:67%;" />
