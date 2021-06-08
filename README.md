# Scratch 3.0 二次开发笔记
Scratch 3.0 二开教程，包教不包会
## 第一步，官方已有克隆之法，不再赘述
## 第二步，明修栈道，暗渡陈仓
- 下面开始喽
### 瞒天过海/李代桃疆/声东击西/以逸待劳
- 1、替换 Logo 图片
    - 法一， 路径：
        - scratch-gui/src/components/menu-bar/
    - 替换文件： 
        - scratch-logo.svg
    - 或 
    - 法二， 打开路径：
        - scratch-gui/src/components/menu-bar/menu-bar.jsx
    - 修改 Logo 文件地址： 
        - import scratchLogo from './scratch-logo.svg';
- 2、替换 favicon 浏览器角标
    - 路径：
        - scratch-gui/static/
    - 替换文件： 
        - favicon.ico
- 3、点击 Logo 返回首页 事件
    - 路径：
        - scratch-gui-develop/src/playground/render-gui.jsx
    - 第11行
        ``` 
        const onClickLogo = () => {
            window.location = '/';
        };
        ```
- 4、关闭‘即将启用’等提示语
    - 路径：
        - scratch-gui-develop/src/components/menu-bar/
    - 文件： 
        - menu-bar.jsx
    - 关键词：
        - MenuBarItemTooltip
        ```
            <MenuBarItemTooltip id="share-button">

            <MenuBarItemTooltip id="community-button">

            <MenuBarItemTooltip id="mystuff">

            <MenuBarItemTooltip
                id="account-nav"
            >
        ```
- 5、取消 Warning: React does not recognize the `isRtl` prop on a DOM element
    - 路径：
        - src/containers/target-pane.jsx
    - 行号：240 ，加入：
        - isRtl,
- 6、禁用书包功能
    - 路径：
        scratch-gui-develop/src/components/gui/gui.jsx
    - 注释以下内容：
        ```
            import Backpack from '../../containers/backpack.jsx';

            {backpackVisible ? (
                <Backpack host={backpackHost} />
            ) : null}
        ```
### 混水摸鱼/抛砖引玉/釜底抽薪/借尸还魂/
- 1、启用 登录功能
    - 路径：
        - src/components/menu-bar/menu-bar.jsx
    - 替换代码范围，行号： 628 - 747
    ```
    {this.props.username ? (
        // ************ user is logged in ************
        <React.Fragment>
            <div className={classNames(
                    styles.menuBarItem,
                    styles.hoverable,
                    styles.accountNavMenu
                )} >
                <span>
                    {this.props.username}
                </span>
                <AccountNav
                    className={classNames(
                        styles.menuBarItem,
                        styles.hoverable,
                        {[styles.active]: this.props.accountMenuOpen}
                    )}
                    isOpen={this.props.accountMenuOpen}
                    isRtl={this.props.isRtl}
                    menuBarMenuClassName={classNames(styles.menuBarMenu)}
                    onClick={this.props.onClickAccount}
                    onClose={this.props.onRequestCloseAccount}
                    onLogOut={this.props.onLogOut}
                />
            </div>
        </React.Fragment>
    ) : (
        <React.Fragment>
            <div className={classNames(
                    styles.menuBarItem,
                    styles.hoverable
                )}
                key="login" onMouseUp={this.props.onClickLogin} >
                <FormattedMessage
                    defaultMessage="Sign in"
                    description="Link for signing in to your Scratch account"
                    id="gui.menuBar.signIn"
                />
                <LoginDropdown
                    className={classNames(styles.menuBarMenu)}
                    isOpen={this.props.loginMenuOpen}
                    isRtl={this.props.isRtl}
                    renderLogin={this.props.renderLogin}
                    onClose={this.props.onRequestCloseLogin}
                />
            </div>
        </React.Fragment>
    )}
    ```
- 2、完善 登录表单页面
    - 路径：
        - src/components/menu-bar/login-dropdown.jsx
    - 行号： 67
        - 登录表单自己写
        - 因为我没使用这个功能。这个是scratch自带的功能
- 2.1、我说下我的登录方式：
    - 路径：
        - src/reducers/
    - 创建 检测登录状态 js 文件
        - user-state.js
    - 具体详见 user-state.js 文件，或者 自己用 ajax、 axios 都可以实现登录
- 3、在 gui.js 中启用启用 登录状态
    - 路径：
        - scratch-gui-develop/src/reducers/gui.js
    - 行号： 30
    ```
    import userStatusReducer, {userStateInitialState} from './user-state';
    ```
    - 行号： 163
    ```
    userStatus: userStatusReducer,
    ```
- 4、在 menu-bar.jsx 中启用 登录状态
    - 路径：
        - src/components/menu-bar/menu-bar.jsx
    - 行号： 67
    ```
    const user = state.scratchGui.userStatus.session;
    ```
- 5、登录后的用户下拉菜单
    - 路径：
        - src\components\menu-bar\account-nav.jsx
    - 搜索关键词：
    ```
    <MenuItemContainer href=
    ```
### 偷梁换柱/反客为主/树上开花/
- 1、更换自己服务器地址
    - 路径：
        - src\lib\project-fetcher-hoc.jsx
    - 修改内容如下：
    ```
    ProjectFetcherComponent.defaultProps = {
        assetHost: 'http://127.0.0.1:5000/static/myscratch',
        projectHost: 'http://127.0.0.1:5000/scratch/project/json'
    };
    ```
- 2、修改 角色、背景资源路径
    - 路径：
        - src/lib/storage.js
    - 修改内容：
    ```
    getAssetGetConfig (asset) {
        return `${this.assetHost}/assets/${asset.assetId}.${asset.dataFormat}`;
    }
    ```
 - 3、修改 ID 分隔符
    - 路径：
        - 
    - 修改内容：
- 4、启用 立即保存和自动保存 功能
    - 路径：
        - 
    - 修改内容：
- 5、保存缩略图
    - 路径：
        - 
    - 修改内容：
- 6、从电脑中打开（导入文件）并保存
    - 路径：
        - 
    - 修改内容：
- 7、手机端虚拟按键实现
    - 功能借鉴于 easy-scratch3 
### Python-Flask 搭建后台
- 1、Flask框架开发后端，整合 scratch
