<template>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>김두현PC</title>
</head>
<body>
    <div id="wrap">
        <div id="header">
            <div id="categories">
                <div class="category_group">
                    <div class="category_menu">
                        <ul class="base">
                            <li class="menu" v-for="(menu, i) in menus" :key="i">
                                <a class="tab" @click="tovisible(menu)">
                                    {{menu}}
                                </a>
                            </li>
                        </ul>
                    </div>
                    <div class="category_more">
                        <ul class="c_more">
                            <li class="sns" v-for="(side_menu, i) in side_menus" :key="i">

                                <a class="tab" :href="side_menu.url">
                                    {{side_menu.name}}
                                </a>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
        <div id="container">
            container(developing....), only writing and phogograph part is literally active.
            <div id="img_container" v-show="visible['전시관']">
                <h1 class="blind">
                    갤러기 결과
                </h1>
                <div class="img_group">
                    <section class="img_each" v-for="(img, i) in images" :key="i">
                        <div class="img_pack">
                            <div class="img_img">
                                <div class="img_img_in">
                                    <img :alt="`imgage${i+1}`" :src="img.url">
                                </div>
                            </div>
                            <div class="img_info">
                                <div class="img_info_place">
                                    {{img.location}}
                                </div>
                                <div class="img_info_title">
                                    {{img.title}}
                                </div>
                                <div class="img_info_detail">
                                    {{images_description[i]}}
                                </div>
                            </div>
                        </div>
                    </section>
                </div>
            </div>
            <div id="wrt_container" v-show="visible['글']">
                <div class="wrt_group">
                    <div class="wrt_group_post">
                        <div class="wrt_group_header">
                            <span class="header">
                                기록, 글, 사진, 소리
                            </span>
                            <div class="deco">
                            </div>
                            <i class="cline"></i>
                        </div>
                        <div class="wrt_group_body">
                            <table class="wrt_post_list">
                                <caption>
                                </caption>
                                <colgroup>
                                    <col class="col_num">
                                    <col class="col_click">
                                    <col class="col_post_title">
                                    <col class="col_date">
                                </colgroup>
                                <tr id="table_header">
                                    <th>
                                        <span class="num">
                                            번호
                                        </span>
                                    </th>
                                    <th>
                                        <span class="click">
                                            조회
                                        </span>

                                    </th>
                                    <th>
                                        <span class="post_title">
                                            제목
                                        </span>
                                    </th>
                                    <th>
                                        <span class="date">
                                            날짜
                                        </span>

                                    </th>
                                </tr>
                                <tr id="each_writing" v-for="(wrt, i) in writings" :key="i">
                                    <td>
                                        <a class="num">
                                            {{wrt.num}}
                                        </a>
                                    </td>
                                    <td>
                                        <span class="click">
                                            {{clicks[i]}}
                                        </span>
                                    </td>
                                    <td>
                                        <a class="post_title" @click="toclick(wrt.num)">
                                            {{wrt.title}}
                                        </a>
                                    </td>
                                    <td>
                                        <span class="date">
                                            {{wrt.date}}
                                        </span>
                                    </td>
                                </tr>
                            </table>
                        </div>
                        <div class="wrt_group_footer">
                            <div class="list_page">
                                <a class="page" href="">1</a>
                                <a class="page" href="">2</a>
                                <a class="page" href="">3</a>
                                <a class="page" href="">4</a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div id="info_container" v-show="visible['소개']">

            </div>
            <div id="visit_container" v-show="visible['방명록']">
  <div class="visitors_group">
    <div id="input_pack">
        <div class="input_box">
          <input type="text" v-model="input_msg" placeholder="작성란" v-on:keyup.enter="addmsg(input_msg)">
        </div>
        <div class="input_button">
          <button @click="addmsg(input_msg)">입력</button>
        </div>
    </div>
    <div id="list_group">
      <table class="visitor_list">
        <caption>
        </caption>
        <colgroup>
          <col class="col_message">
          <col class="col_date">
        </colgroup>
        <tr id="each_writing" v-for="(msg, i) in messages" :key="i">
          <td>
            <p class="post_title">
              {{msg.message}}
            </p>
          </td>
          <td>
            <p class="date">
              {{msg.date}}
            </p>
          </td>
        </tr>
      </table>
    </div>
  </div>

            </div>
        </div>
    </div>
</body>
</html>
</template>

<script>

export default {
  data(){
    return{
        menus : ['소개', '글', '전시관', '방명록'],
        side_menus : [  {name: '인스타', url: 'https://www.instagram.com/_dudududukim/', visiable: true},
                        {name: '블로그', url: 'https://blog.naver.com/rlaengux', visiable: true},
                        {name: '관리자', url: '', visiable: false},
                        {name: '로그인', url:'', visiable: true},],
        /** 나중에 active side menu를 만들어 visible을 이용하자 **/
        images :[
            {title: '제주도',location: 'Jeju_Island (KR)', description: '',url: require('./assets/img/section1.jpg')},
            {title: '바다와 파도',location: 'Busan (KR)', description: '',url: require('./assets/img/section2.jpg')},
            {title: '경복궁 경회루',location: 'Seoul(KR)', description: '',url: require('./assets/img/section3.jpg')},
            {title: '경복궁 경회루\n(야간)',location: 'Seoul(KR)', description: '',url: require('./assets/img/section4.jpg')},
        ],
        images_description : ['This is the A-cup of my jeju travel.<br>It was really tough day but this photo gives us kind of coziness.<br>This might be pure function of photograph.',
                              'This might be my favorite shots through GR#.<br>Although this photo is crop, it has really sharp details presenting dynamic waves and the color balance is surely warm.',
                              'While snowing hardly, the spark was initally started pushing me way out home.<br>I could see them most beautiful scape of gyeongbukgong.',
                              'It was a tough day. I was expecting the touches that palace would give me but it was just crowded people in the palace'],
        writings : [
            {num : 5, clicks: 0, title: 'title5_euhubxn', date: '2022.05.12'},
            {num : 4, clicks: 0, title: 'title4_wesxdfwexn', date: '2021.12.11'},
            {num : 3, clicks: 0, title: 'title3_xdfwesdf', date: '2021.11.31'},
            {num : 2, clicks: 0, title: 'title2_oqm;xcv', date: '2020.09.08'},
            {num : 1, clicks: 0, title: 'title1_first', date: '2020.07.20'},
            ],
        messages : [],
        input_msg :'',
        visible : {'전시관' : false, '글': false, '방명록': false, '소개' : false},
        clicks : [0, 0, 0, 0, 0]
    }
  },
  methods :{
      tovisible(menu){
              for(var i in this.visible){
                  if(i === menu) this.visible[i] = true;
                  else this.visible[i] = false;
              }
          console.log(this.visible);
      },
      toclick(num){
            console.log(num);
            this.clicks[this.writings.length - num]++;
      },
      addmsg(msg){
          let today = new Date();
          var inputmsg = {date: today.toLocaleDateString(), message: msg};
          this.messages.unshift(inputmsg);
          this.input_msg = '';
      },
  }
}
</script>

<style>
@import "./assets/css/main.css"
</style>
