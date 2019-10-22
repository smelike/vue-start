<div class="channel-wrapper">
	<div>
	  <div style="padding-bottom: 6px;border-bottom: 1px solid #ddd;">
		<span class="el-icon-chat-line-round channel-icon">{{ selectedGroup.name }}</span>
		<el-button v-if="selectedGroup.name !== 'general'" icon="el-icon-plus" size="mini">添加新成员</el-button>
	  </div>
	</div>
	<div class="channel-body">
	  <div class="channel-meta">
		<span style="display: inline-block;padding-top: 10px;">{{ selectedGroup.desc }}</span>
		<el-divider></el-divider>
	  </div>
	  <div class="channel-content">
		<div class="channel-msg">
		  <section v-if="messageList.length > 0">
		  <ul class="chat-content-list" v-loading="messageLoading">
			<li class="chat-item" v-for="(item, index) in messageList" :key="index">
			  <div class="chat-item">
				<div v-bind:class="[  item.username === userName ? 'mychat' : 'otherchat' ]">
				  <!-- <div class="userAvatar" style="text-align: center; width: 40px; height: 40px; border-radius: 50%; line-height: 40px; color: white; display: inline-block;">
					<img style="width: 40px; height: 40px; border-radius: 50%;" src="https://avatars1.githubusercontent.com/u/24861316?v=4" alt="aermin">
				  </div> -->
				  <div class="nt">
					<span style="color: #333;">{{ item.username }}</span>
					<span style="margin-left: 10px;">{{ item.created_at }}</span>
				  </div>
				  <div class="msg-render" style="color: #333;" v-html="item.message"></div>
				</div>
			  </div>
			</li>
		  </ul>
		  </section>
		  <section v-else>暂无聊天记录</section>
		</div>
	  </div>
	</div>
	<div class="input-msg">
	  <el-input type="textarea" placeholder="请输入所要发送的信息" v-model="inputMessage" class="input-msg-box"></el-input>
	  <p class="btn"><el-button type="primary" @click="publishMessage">发送</el-button></p>
	</div>
</div>


<style>

.chat-wrapper {
  height: 100%;
  position: relative;
}

.chat-aside {
  border-right: 1px solid #ddd;
}
.chat-header {
  height: 50px;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  padding: 20px;
}
.chat-list {
  margin-top: 10px;
}
.chat-list li {
  float: none;
}
.chat-list li a {
  display: block;
  border-radius: 0;
  color: #666;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  position: relative;
  padding: 11px 0 11px 30px;
  line-height: 23px;
  border-right: 4px solid transparent;
}
.chat-list li.active a {
  background: #e7f9f6;
  color: #22d7bb;
  border-right: 4px solid #22d7bb;
}

.chat-list li a span.close-icon {
  display: none;
}

.chat-body .chat-list li:hover a span.close-icon {
  display: inline;
}
.close-icon {
  font-size: 16px;
  position: relative;
  right: -10px;
  color: #aaa;
}
.channel-icon {
  line-height: 20px;
  text-align: center;
  margin-right: 10px;
  font-weight: bold;
  font-size: 24px;
}

.channel-wrapper {
  height: 100%;
  width: 100%;
}
.channel-meta {
  /* padding: 20px 25px 0px 25px; */
  color: #b9b9b9;
  font-size: 15px;
}

.channel-content {
  height: calc(100% - 100px);
  overflow: auto;
}
.channel-msg-date-time {
  color: #b9b9b9;
}
.channel-body {
  /* margin: 10px 20px; */
  background-color: #fff;
  height: calc(100% - 104px);
}
.chat-content-list {
  height: calc(100% - 20px);
  padding: 20px 0;
  display: flex;
  flex-direction: column;
  list-style: none;
  overflow-y: auto;
}
.chat-item {
  width: 100%;
  margin: 4px 0;
  color: #b9b9b9;
}
.chat-item .mychat {
  width: 100%;
  position: relative;
}
.chat-item .mychat .nt {
  font-size: 14px;
  right: 60px;
  position: absolute;
  color: #686868;
}
.chat-item .mychat .userAvatar {
  right: 10px;
}
.chat-item .mychat .msg-render {
  float: right;
  margin-right: 20px;
  padding: 6px 8px;
  background: #daf4fe;
  border-radius: 6px;
}
.chat-item .otherchat {
  width: 100%;
  position: relative;
}

.chat-item .otherchat .userAvatar {
  left: 10px;
  cursor: pointer;
}
.chat-item .userAvatar {
  position: absolute;
  top: 50%;
  transform: translateY(-50%)
}
.chat-item .otherchat .nt {
  font-size: 14px;
  left: 20px;
  /* top: -26px; */
  position: absolute;
  color: #686868;
}
.chat-item .otherchat .msg-render {
  float: left;
  margin-left: 20px;
  padding: 6px 8px;
  background-color: #f3f3f3;
  border-radius: 6px;
}
.chat-item .msg-render {
  font-size: 14px;
  word-wrap: break-word;
  max-width: 50%;
  margin-top: 18px;
}

.input-msg {
  /* height: 20px; */
  /* position: absolute; */
  display: flex;
  background-color: #f3f3f3;
  bottom: 0px;
  width: 100%;
  padding: 4px 10px;
}
</style>