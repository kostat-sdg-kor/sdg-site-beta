---
layout: page
language: en
permalink: /en/publications/
---
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
<script>
//    페이지 로드 시 페이징 처리
   $(document).ready(function(){
      contentShow();
      createPage();
      
   });

   var isSearch = false;
   
   function contentShow(){
      var content = $(".content");
      for(var i=0; i < content.length; i++){
         if(i < 8){
            content.eq(i).css("display", "table-row");
         }else{
            content.eq(i).css("display", "none");
         }
      }
   }
   
   function createPage(){
      $(".pagination").remove();
      $(".page_form").append("<ul class='pagination'></ul>");
      var content = $(".content");
      
      var liCount = Math.ceil(content.length/8);
      for(var i=1; i <= liCount; i++){
         if(i==1){
            $(".pagination").append("<li onclick='changePage(this.innerHTML)' class='pageLi on'>"+i+"</li>");
         }else{
            $(".pagination").append("<li onclick='changePage(this.innerHTML)' class='pageLi'>"+i+"</li>");
         }
      }
   }
   
//    검색 기능
   function search(){
      isSearch = true;
      var value = $(".srh_input").val();
      var title = $(".title");
      
      for(var i=0; i < title.length; i++){
         $(".content").eq(i).attr("class", "content");
         $(".content").eq(i).css("display", "none");
         
         if(title[i].innerHTML.indexOf(value) != -1){
            $(".content").eq(i).attr("class", "content isSearch");
         }
      }
      
      searchShow();
      searchPage();
   }
   
   function searchShow(){
      var content = $(".isSearch");
      var count = 0;
      while(count < 8){
         if(content.length == count){
            break;
         }else{
            content.eq(count).css("display", "table-row");
            count++;
         }
      }      
   }
   
   function searchPage(){
      
      $(".pagination").remove();
      $(".page_form").append("<ul class='pagination'></ul>");
      
      var content = $(".isSearch");
      
      createGaraData("isSearch");
      
      var liCount = Math.ceil(content.length/8);
      
      for(var i=1; i <= liCount; i++){
         if(i==1){
            $(".pagination").append("<li onclick='changePage(this.innerHTML)' class='pageLi on'>"+i+"</li>");
         }else{
            $(".pagination").append("<li onclick='changePage(this.innerHTML)' class='pageLi'>"+i+"</li>");
         }
      }
      
      $(".report1_btn").css("background", "gray");
      $(".report2_btn").css("background", "gray");
      $(".report3_btn").css("background", "gray");
   }
   
//    페이징 처리
   function changePage(index){
      if(isSearch){
         var content = $(".isSearch");
         
         for(var i=0; i < content.length; i++){
            if(i >= 8*(index-1) && i < 8*index){
               content.eq(i).css("display", "table-row");
            }else{
               content.eq(i).css("display", "none");
            }
         }
         
         createGaraData("isSearch");
         
         $(".pageLi").each(function(number, value){
            if(index-1 == number){
               $(".pageLi").eq(number).attr("class", "pageLi on");
            }else{
               $(".pageLi").eq(number).attr("class", "pageLi");
            }
         });
         
      }else{
         var content = $(".content");
         for(var i=0; i < content.length; i++){
            if(i >= 8*(index-1) && i < 8*index){
               content.eq(i).css("display", "table-row");
            }else{
               content.eq(i).css("display", "none");
            }
         }
         
         createGaraData("content");
         
         $(".pageLi").each(function(number, value){
            if(index-1 == number){
               $(".pageLi").eq(number).attr("class", "pageLi on");
            }else{
               $(".pageLi").eq(number).attr("class", "pageLi");
            }
         });         
         
      }
      
   }
   
   function reportView(item){
      isSearch = true;
      $(".srh_input").val("");
      var content = $(".content");
      for(var i=0; i < content.length; i++){
         content.eq(i).attr("class", "content");
         content.eq(i).css("display", "none");
      }
      
      var report = $("."+item);
      
      for(var i=0; i < report.length; i++){
         var parent = report[i].parentNode;
         parent.className = "content isSearch";
      }
      
      searchShow();
      searchPage();
      
      createGaraData("isSearch");
      
      
      $(".report1_btn").css("background", "gray");
      $(".report2_btn").css("background", "gray");
      $(".report3_btn").css("background", "gray");
      
      var click_btn = $("."+item+"_btn");
      
      click_btn.css("background", "#5D5D5D");
   }
   
   function createGaraData(data){
      $(".gara").remove();
      var content = $("."+data);
      var count = 0;
      content.each(function(i, value){
         if(content.eq(i).css("display") == "table-row"){
            count++;
         }
      });
      
      var str = "";
      str += "<tr class='gara'>";
      str += "<td></td>";
      str += "<td></td>";
      str += "<td></td>";
      str += "</tr>";
      
      if(8-count != 0){
         for(var i=0; i < (8-count); i++){
            $(".board_table").append(str);
         }
      }else{
         $(".gara").remove();
      }
   }
</script>
<style>
@media ( min-width: 768px ){
   /*  공통 */
      body { padding:0; margin:0; }
      a { text-decoration:none; } 
   /*    상단 제목검색 및 버튼 CSS */
      input[type=button]:hover { background:#5D5D5D; transition : all ease 0.5s 0s; cursor:pointer; }
      input[type=button]:visited { background:#5D5D5D; }
      
      .search_form { text-align : center; width:100%; height: 100px;   background : #BDBDBD; }
      
      .search_form .search_div { display : inline-block; width : 350px; background : #ffffff; margin-top : 30px; }
      .search_form .search_div .srh_input { font-size : 16px; width: 80%; height : 100%; padding : 10px; margin : 0px; border: 0px; outline : none; float:left; }
      .search_form .search_div .srh_btn {   width: 70px; height: 40px; border: 0px; background : #FF4848; outline : none; color: #ffffff; float:right; margin:0px;   }
       
       .report_div { display : inline-block; width : 100%; height: 40px; text-align:center; margin-bottom: 20px;}
       .report1_btn, .report2_btn, .report3_btn { font-size:10pt; height: 40px; outline : none; background : gray; border : 0px; color : #ffffff; margin-right : 10px; border-radius:10px;}
       
       
   /*  하단 게시판 CSS  */
      .board_form { margin : 20px 5% 0;}
      .board_form .board_table { width : 100%; border-collapse : collapse; border-bottom : 1px solid black; }
      .board_form .board_table .board_title { border-top : 2px solid black; border-bottom : 1px solid black;}
      .board_form .board_table tr:not(:first-child) { border-top : 1px dotted black; }
      .board_form .board_table tr:last-child { border-bottom : 1px solid black; }
      .board_form .board_table tr { height : 50px;}
      .board_form .board_table .board_title th { text-align : center; }
      .board_form .board_table tr td:nth-child(1) { padding-left : 10px; }
      .board_form .board_table tr td:nth-child(2), td:nth-child(3) { text-align : center; }
      
   /*  하단 페이징 CSS  */   
      .board_form .page_form { text-align : center; }
      .board_form .page_form .pagination { list-style: none; font-size:14pt; }
      .board_form .page_form .pagination li { display : inline-block; cursor : pointer; padding:0 10px 0; margin:0 5px; border: 1px solid #BDBDBD; border-radius : 25px; }
      .board_form .page_form .pagination li:hover { background:#6799FF; transition : all ease 0.5s 0s; color : #ffffff; }
      
      .on { background:#6799FF; color:#ffffff; }
      
      .top_div { text-align : center; width:99%; border:0; font-weight:bold;}
      .top_div .item { display:inline-block; width:250px; padding: 5px 5px 0px 0px;}
      .top_div .item a img { border:1px solid black; border-radius:5px 5px 5px 5px; width:150px; height:215px; }
}
         
   @media ( max-width: 767px ){
      /*  공통 */
         body { padding:0; margin:0; }
      /*    상단 제목검색 및 버튼 CSS */
         input[type=button]:hover { background:#5D5D5D; transition : all ease 0.5s 0s; cursor:pointer; font-size:12pt;}
         input[type=button]:visited { background:#5D5D5D; }
         
         .search_form { text-align : center; width:100%; height: 100px;   background : #BDBDBD; }
         
         .search_form .search_div { display : inline-block; width : 350px; background : #ffffff; margin-top : 30px; }
         .search_form .search_div .srh_input { font-size : 15px; width: 80%; height : 100%; padding : 10px; margin : 0px; border: 0px; outline : none; float:left; }
         .search_form .search_div .srh_btn {   width: 70px; height: 40px; border: 0px; background : #FF4848; outline : none; color: #ffffff; float:right; margin:0px;   }
          
          .report_div { display : inline-block; width: 100%; text-align:center; margin-bottom: 20px;}
          .report1_btn, .report2_btn, .report3_btn { display: block; width: 100%; height: 40px; font-size:11pt; outline : none; background : gray; border : 0px; color : #ffffff;}
          
          
      /*  하단 게시판 CSS  */
         .board_form { margin : 20px 5% 0;}
         .board_form .board_table { width : 100%; border-collapse : collapse; border-bottom : 1px solid black; }
         .board_form .board_table .board_title { border-top : 2px solid black; border-bottom : 1px solid black;}
         .board_form .board_table tr:not(:first-child) { border-top : 1px dotted black; }
         .board_form .board_table tr:last-child { border-bottom : 1px solid black; }
         .board_form .board_table tr { height : 50px;}
         .board_form .board_table .board_title th { text-align : center; }
         .board_form .board_table tr td:nth-child(1) { padding-left : 10px; }
         .board_form .board_table tr td:nth-child(2), td:nth-child(3) { text-align : center; }
         
      /*  하단 페이징 CSS  */   
         .board_form .page_form { text-align : center; }
         .board_form .page_form .pagination { list-style: none; font-size:14pt; }
         .board_form .page_form .pagination li { display : inline-block; cursor : pointer; padding:0 10px 0; margin:0 5px; border: 1px solid #BDBDBD; border-radius : 25px; }
         .board_form .page_form .pagination li:hover { background:#6799FF; transition : all ease 0.5s 0s; color : #ffffff; }
         
         .on { background:#6799FF; color:#ffffff; }
         
         .top_div { text-align : center; width:100%; border:0; font-weight:bold;}
         .top_div .item { display:inline-block; width:400px;}
         .top_div .item a img { border:1px solid black; border-radius:5px 5px 5px 5px; width:150px; height:215px; }
   }
</style>

<br/>
   
   <div class="top_div">
   <div class="item">
      <div>
         <a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/2023_report_en.pdf">
            <img src="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/2023_en.png" alt="1"/>
         </a>
      </div>
      <div>
         <p> SDG in the ROK Progress Report 2023<br></p>
      </div>
   </div>
      
 
   
      <div class="item">
      <div>
         <a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/The-Sustainable-Development-Goals-Report-2022.pdf">
             <img src="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/UN-2022.png" alt="2"/>    
          </a>
      </div>
      <div>
         <p>The Sustainable Development Goals Report 2022<br></p>
      </div>
   </div>   
      
   <div class="item">
      <div>
         <a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/VNR.pdf">
            <img src="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/VNR.png" alt="3"/>
         </a>
      </div>
      <div>
         <p>National Voluntary Review Report 2016<br></p>
      </div>
   </div>
</div>
<div class="search_form">
   <div class="search_div">
      <input type="text" class="srh_input" name="search_input" placeholder=" "/>
      <input type="button" class="srh_btn" name="search_button" value="search" onclick="search();"/>
   

   </div>
</div>

<div class="board_form">
   <div class="report_div">
      <input type="button" class="report1_btn" onclick="location.reload();" value="　　All　　">
      <input type="button" class="report1_btn" onclick="reportView('report1');" name="report1" value="SRI Reports"/>
      <input type="button" class="report2_btn" onclick="reportView('report2');" name="report2" value="Other Agencies Reports"/>
      <input type="button" class="report3_btn" onclick="reportView('report3');" name="report3" value="UN Reports"/>      
   </div>

   <table class="board_table">
      <tr class="board_title">
         <th>Title</th>
         <th>Agency</th>
         <th>Year</th>
      </tr>


 <tr class="content"><!-- 9 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/SDG forum 2023.pdf">[Poster] The SDG Data Innovation Forum 2023</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2023</td>
      </tr>

      
       <tr class="content"><!-- 8 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/2023_report_en.pdf">SDG in the ROK Progress Report 2023</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2023</td>
      </tr>
      
        <tr class="content"><!-- 7 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/2023_report_ko.pdf">한국의 SDG 이행보고서 2023</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2023</td>
      </tr>

     
 <tr class="content"><!-- 6 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/2022forum_eng.pdf">[Poster] The 1st SDG Data Innovation Forum</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2022</td>
      </tr>
      
       <tr class="content"><!-- 5 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/The-Sustainable-Development-Goals-Report-2022.pdf">The Sustainable Development Goals Report 2022</a></td>
         <td class="report3">United Nations</td>
         <td>2022</td>
      </tr>  
      
      <tr class="content"><!-- 4 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/k-report2022.pdf">한국의 SDGs 이행보고서 2022</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2022</td>
      </tr>

      
      <tr class="content"><!-- 3 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/e-report2022.pdf">SDGs in the ROK Progress Report 2022</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2022</td>
      </tr>
      
      <tr class="content"><!-- 2 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/un-report2021.pdf">The Sustainable Development Goals Report 2021</a></td>
         <td class="report3">United Nations</td>
         <td>2021</td>
      </tr>
      <tr class="content"><!--1 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/press1.pdf">[보도자료] 한국 SDGs 데이터 플랫폼 영문 서비스 개시</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2021</td>
      </tr>
      
      <tr class="content"><!-- 2 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/press2.pdf">[Press Release] KOSTAT launches the Korean SDGs Data Platform</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2021</td>
      </tr>
      
      <tr class="content"><!-- 3 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/16.pdf">한국의 SDGs 이행보고서 2021</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2021</td>
      </tr>
      
      <tr class="content"><!-- 4 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/17.pdf">SDGs in the ROK Progress Report 2021</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2021</td>
      </tr>
      
      <tr class="content"><!-- 5 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/15.pdf">SDGs 지표 톺아보기</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2020</td>
      </tr>
      
      <tr class="content"><!-- 6 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/5_2020.pdf">세분화된 데이터 생산을 위한 다양한 접근법 탐색-장애,도시,교통 부문</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2020</td>
      </tr>
      <tr class="content"><!-- 7 -->
         <td class="title"><a href="https://unstats.un.org/sdgs/report/2020/The-Sustainable-Development-Goals-Report-2020.pdf">The Sustainable Development Goals Report 2020</a></td>
         <td class="report3">United Nations</td>
         <td>2020</td>
      </tr>

      <tr class="content"><!-- 8 -->
         <td class="title"><a href="https://www.unescap.org/sites/default/files/publications/ESCAP_Asia_and_the_Pacific_SDG_Progress_Report_2020.pdf">Asia and the Pacific SDG Progress Report 2020</a></td>
         <td class="report3">UN ESCAP</td>
         <td>2020</td>
      </tr>      
      
      <tr class="content"><!-- 9 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/1.pdf">한국의 SDGs 데이터와 이행현황</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2019</td>
      </tr>

      <tr class="content"><!-- 10 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/2.pdf">SDGs in the ROK Progress Report 2019</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2019</td>
      </tr>

      <tr class="content"><!-- 11 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/1572586046142_K-SDGs_report.pdf">2019 국가 지속가능발전목표(K-SDGs) 수립보고서</a></td>
         <td class="report2">환경부 지속가능발전위원회</td>
         <td>2019</td>
      </tr>

      <tr class="content"><!-- 12 -->
         <td class="title"><a href="https://www.unesco.or.kr/assets/data/report/kUBzCt7Rs5swF6lB10Zg5c5AFRroz2_1573104458_2.pdf">포용성 증진을 위한 교육과 도시</a></td>
         <td class="report2">유네스코한국위원회</td>
         <td>2019</td>
      </tr>

      <tr class="content"><!-- 13 -->
         <td class="title"><a href="https://www.unesco.or.kr/assets/data/report/JPZCFQ3y82b98Bm5tkJgwIstZ3HneT_1573104541_2.pdf">SDG4-교육2030 포용성과 교육에 관한 연구 보고서</a></td>
         <td class="report2">유네스코한국위원회, 한국교육개발원</td>
         <td>2019</td>
      </tr>
      
      <tr class="content"><!-- 14 -->
         <td class="title"><a href="https://www.unesco.or.kr/assets/data/report/Lg0UTQ7aY1amLxfWLkvfPyTO35u6XY_1567147136_2.pdf">한국의 SDG4 이행 현황 연구</a></td>
         <td class="report2">한국교육개발원</td>
         <td>2019</td>
      </tr>

      <tr class="content"><!-- 15 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/49.pdf">글로벌 여성의제 국내이행 점검</a></td>
         <td class="report2">한국여성정책연구원</td>
         <td>2019</td>
      </tr>

      <tr class="content"><!-- 16 -->
         <td class="title"><a href="https://library.kei.re.kr:444/dmme/img/001/005/028/%ec%a7%80%ec%86%8d%ea%b0%80%eb%8a%a5%eb%b0%9c%ec%a0%84%ea%b3%bc%ec%97%90%eb%84%88%ec%a7%80%ec%82%b0%ec%97%85%ec%a0%84%ed%99%98%ea%b8%b0%ed%9b%84%eb%b3%80%ed%99%94%ec%a0%95%ec%b1%85%eb%aa%a9%ed%91%9c1.5%eb%8f%84%eb%8c%80%ec%9d%91%ec%9d%84%ec%a4%91%ec%8b%ac%ec%9c%bc%eb%a1%9c_%ec%9d%b4%ec%b0%bd%ed%9b%88.pdf">지속가능발전과 에너지·산업전환 : 기후변화 정책목표 1.5℃ 대응을 중심으로</a></td>
         <td class="report2">한국환경정책평가연구원</td>
         <td>2019</td>
      </tr>

      <tr class="content"><!-- 17 -->
         <td class="title"><a href="https://www.unesco.or.kr/assets/data/report/Tiop5H5KP4p8xfZ65chbYUviB6h3Bg_1572326682_2.pdf">우리의 지속가능한 해양</a></td>
         <td class="report2">유네스코한국위원회</td>
         <td>2019</td>
      </tr>


      <tr class="content"><!-- 18 -->
         <td class="title"><a href="http://know.nifos.go.kr/book/search/DetailView.ax?&cid=173483">지속가능발전목표(SDGs) 이행을 위한 자발적 국가평가(VNR) 분석 : SDG 15(육상생태계)를 중심으로</a></td>
         <td class="report2">국립산림과학원</td>
         <td>2019</td>
      </tr>

      <tr class="content"><!-- 19 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/KOICA_73.pdf">SDG16(평화) 논의 및 이행현황 분석: 한국과 국제기구를 중심으로</a></td>
         <td class="report2">한국국제협력단(KOICA)</td>
         <td>2019</td>
      </tr>

      <tr class="content"><!-- 20 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/82.pdf">국제협력 비전, 전략, 추진체계 : 국제개발협력을 중심으로</a></td>
         <td class="report2">경제인문사회연구회</td>
         <td>2019</td>
      </tr>    

      <tr class="content"><!-- 21 -->
         <td class="title"><a href="https://unstats.un.org/sdgs/report/2019/The-Sustainable-Development-Goals-Report-2019.pdf">The Sustainable Development Goals Report 2019</a></td>
         <td class="report3">United Nations</td>
         <td>2019</td>
      </tr>

      <tr class="content"><!-- 22 -->
         <td class="title"><a href="https://sustainabledevelopment.un.org/content/documents/24797GSDR_report_2019.pdf">Gobal Sustainable Development Report 2019</a></td>
         <td class="report3">United Nations</td>
         <td>2019</td>
      </tr>

      <tr class="content"><!-- 23 -->
         <td class="title"><a href="https://www.unescap.org/sites/default/files/publications/ESCAP_Asia_and_the_Pacific_SDG_Progress_Report_2019.pdf">Asia and the Pacific SDG Progress Report 2019</a></td>
         <td class="report3">UN ESCAP</td>
         <td>2019</td>
      </tr>

       <tr class="content"><!-- 24 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/RR2019-20.pdf">지속가능개발목표(SDGs) 달성을 위한 교육개발 협력 연구(III): 고등교육 실천 전략 (2019)</a></td>
         <td class="report2">한국교육개발원</td>
         <td>2019</td>
      </tr>

      <tr class="content"><!-- 25 -->
         <td class="title"><a href="https://www.unesco.or.kr/assets/data/report/iqn7PJJd2HUioDtVDGTz7aVlBgIN5u_1545633687_2.pdf">SDGs와 한반도 평화</a></td>
         <td class="report2">유네스코한국위원회</td>
         <td>2018</td>
      </tr>

      <tr class="content"><!-- 26 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/14.pdf">한·중 유엔 지속가능발전목표(SDGs) 이행 비교 및 협력방안</a></td>
         <td class="report2">한국대외경제정책연구원</td>
         <td>2018</td>
      </tr>

      <tr class="content"><!-- 27 -->
         <td class="title"><a href="http://www.klri.re.kr/viewer/skin/doc.html?fn=6%ED%98%B8_UN%EC%9D%98%20%EC%A7%80%EC%86%8D%EA%B0%80%EB%8A%A5%EB%B0%9C%EC%A0%84%EB%AA%A9%ED%91%9C-%EB%B9%88%EA%B3%A4%EA%B3%BC%20%EB%B6%88%ED%8F%89%EB%93%B1.pdf&rs=/doc_convert/FILE_0000000000261036Jfvl">SDGs 시대, 공유가치창출(CSV)과 비즈니스기회: 신흥국 진출 전략</a></td>
         <td class="report2">한국법제연구원</td>
         <td>2018</td>
      </tr>

      <tr class="content"><!-- 28 -->
         <td class="title"><a href="https://www.krei.re.kr/krei/researchReportView.do?key=67&pageType=010101&biblioId=518120&pageUnit=10&searchCnd=all&searchKrwd=SDGs%20%EB%8B%AC%EC%84%B1%EC%9D%84%20%EC%9C%84%ED%95%9C%20%EB%86%8D%EB%A6%BC%EB%B6%84%EC%95%BC%20ODA%20%EC%A4%91%EC%9E%A5%EA%B8%B0%20%EC%A0%84%EB%9E%B5&pageIndex=1&engView=">SDGs 달성을 위한 농림분야 ODA 중장기 전략</a></td>
         <td class="report2">한국농촌경제연구원</td>
         <td>2018</td>
      </tr>

      <tr class="content"><!-- 29 -->
         <td class="title"><a href="https://www.unesco.or.kr/assets/data/report/4Q03otQgPqVWaO6UqAnmELZtei28UL_1531982225_2.pdf">문답으로 풀어보는 지속가능발전목표(SDG)4 교육 2030</a></td>
         <td class="report2">유네스코한국위원회</td>
         <td>2018</td>
      </tr>
            
      <tr class="content"><!-- 30 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/37.pdf">지속가능개발목표(SDGs) 달성을 위한 교육개발협력연구(Ⅱ): 직업교육훈련(TVET) 실천 전략</a></td>
         <td class="report2">한국교육개발원</td>
         <td>2018</td>
      </tr>


      <tr class="content"><!-- 31 -->
         <td class="title"><a href="http://www.klri.re.kr/viewer/skin/doc.html?fn=12%ED%98%B8_%EC%A7%80%EC%86%8D%EA%B0%80%EB%8A%A5%EB%B0%9C%EC%A0%84%EB%AA%A9%ED%91%9C%20%EC%8B%A4%ED%98%84%EC%9D%84%20%EC%9C%84%ED%95%9C%20%ED%8A%B9%EC%88%98%EA%B5%90%EC%9C%A1%EB%B2%95%EC%A0%9C%20%EA%B0%9C%EC%84%A0%EB%B0%A9%EC%95%88.pdf&rs=/doc_convert/FILE_000000000026098Y6ZtM">지속가능발전목표(SDGs) 실현을 위한 특수교육법제 개선방안</a></td>
         <td class="report2">한국청소년정책연구원</td>
         <td>2018</td>
      </tr>


      <tr class="content"><!-- 32 -->
         <td class="title"><a href="http://www.klri.re.kr/viewer/skin/doc.html?fn=7%ED%98%B8_%EC%A7%80%EC%86%8D%EA%B0%80%EB%8A%A5%EB%B0%9C%EC%A0%84%EB%AA%A9%ED%91%9C%EB%82%B4%205%EB%B2%88%20%EC%84%B1%ED%8F%89%EB%93%B1%20%EB%8F%85%EC%9E%90%EB%AA%A9%ED%91%9C%EC%9D%98%20%EC%A0%A0%EB%8D%94%EC%A0%81%20%EA%B4%80%EC%A0%90%EC%9D%98%20%ED%95%B4%EC%84%9D%EA%B3%BC%20%EA%B5%AD%EB%82%B4%20%EC%9D%B4%ED%96%89%20%EB%B0%A9%EC%95%88.pdf&rs=/doc_convert/FILE_000000000026105HIulh">지속가능발전목표(SDGs) 내 5번 성평등 독자목표의 젠더적 관점의 해석과 국내 이행 방안</a></td>
         <td class="report2">한국법제연구원</td>
         <td>2018</td>
      </tr>

      <tr class="content"><!-- 33 -->
         <td class="title"><a href="http://www.klri.re.kr/viewer/skin/doc.html?fn=11%ED%98%B8_%EC%A7%80%EC%86%8D%EA%B0%80%EB%8A%A5%EB%B0%9C%EC%A0%84%EB%AA%A9%ED%91%9C%EC%99%80%20%EC%97%AC%EC%84%B1%EB%85%B8%EC%9D%B8%EC%9D%B8%EA%B6%8C.pdf&rs=/doc_convert/FILE_000000000026096CSHFX">지속가능발전목표(SDGs)와 여성노인인권</a></td>
         <td class="report2">한국법제연구원</td>
         <td>2018</td>
      </tr>

      <tr class="content"><!-- 34 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/50.pdf">지속가능발전목표(SDGs) 내 성평등 관련 지표의 국내이행 현황 및 정책과제</a></td>
         <td class="report2">한국여성정책연구원</td>
         <td>2018</td>
      </tr>

      <tr class="content"><!-- 35 -->
         <td class="title"><a href="http://www.klri.re.kr/viewer/skin/doc.html?fn=CC18-17-11.pdf&rs=/doc_convert/FILE_000000000026677uDqF9">기후변화와 지속가능발전 법제연구: 산업 - 산업분야 지속가능발전목표(SDGs) 국내이행의 이해와 촉진 -</a></td>
         <td class="report2">한국법제연구원</td>
         <td>2018</td>
      </tr>


      <tr class="content"><!-- 36 -->
         <td class="title"><a href="http://www.klri.re.kr/viewer/skin/doc.html?fn=CC18-17-8.pdf&rs=/doc_convert/FILE_000000000026672JvqEw">기후변화와 지속가능발전 법제연구 : 보건·복지 - 보건의료기본법 상의 기후변화에 따른 국민건강영향평가 -</a></td>
         <td class="report2">한국법제연구원</td>
         <td>2018</td>
      </tr>

      <tr class="content"><!-- 37 -->
         <td class="title"><a href="https://library.kei.re.kr:444/dmme/img/001/005/027/%ec%a7%80%ec%86%8d%ea%b0%80%eb%8a%a5%eb%b0%9c%ec%a0%84%eb%aa%a9%ed%91%9cSDGs%ec%99%80%ea%b8%b0%ed%9b%84%eb%b3%80%ed%99%94%ea%b5%ad%ea%b0%80%ec%9e%90%eb%b0%9c%ec%a0%81%ea%b3%b5%ec%95%bdNDC%ec%97%b0%ea%b3%84_%ea%b9%80%ed%98%b8%ec%84%9d.pdf">지속가능한발전목표(SDGs)와 기후변화 국가자발적공약(NDC) 연계이행에 대한 연구</a></td>
         <td class="report2">한국환경정책평가연구원</td>
         <td>2018</td>
      </tr>

      <tr class="content"><!-- 38 -->
         <td class="title"><a href="http://www.klri.re.kr/viewer/skin/doc.html?fn=CC18-17-12.pdf&rs=/doc_convert/FILE_000000000026678VZ8po">기후변화와 지속가능발전 법제연구: 해양 - 해양분야 지속가능발전목표(SDGs) 국내이행 촉진을 위한 정책방향 -</a></td>
         <td class="report2">한국법제연구원</td>
         <td>2018</td>
      </tr>

      <tr class="content"><!-- 39 -->
         <td class="title"><a href="https://www.unesco.or.kr/assets/data/report/m8xCs1z3ObBt4D81Dax9c2KyIXMHnB_1543384964_2.pdf">우리의 지속가능한 생물다양성</a></td>
         <td class="report2">유네스코한국위원회</td>
         <td>2018</td>
      </tr>

      <tr class="content"><!-- 40 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/KOICA_74.pdf">SDG16달성을 위한 KOICA 이행방안</a></td>
         <td class="report2">한국국제협력단(KOICA)</td>
         <td>2018</td>
      </tr>

      <tr class="content"><!-- 41 -->
         <td class="title"><a href="http://www.klri.re.kr/viewer/skin/doc.html?fn=CC18-17-7.pdf&rs=/doc_convert/FILE_000000000026670AfwwM">기후변화와 지속가능발전 법제연구 : 제도 - SDGs 이행을 위한 국내 법체계 개선방안 -</a></td>
         <td class="report2">한국법제연구원</td>
         <td>2018</td>
      </tr>

      <tr class="content"><!-- 42 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/77.pdf">개도국 SDGs 이행 지원을 위한 개발재원 확대방안</a></td>
         <td class="report2">대외경제정책연구원</td>
         <td>2018</td>
      </tr>
           
      <tr class="content"><!-- 43 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/81.pdf">SDGs 도입 이후 개도국 협력전략과 대응과제 : 무역과 기후변화의 정책일관성을 중심으로</a></td>
         <td class="report2">대외경제정책연구원</td>
         <td>2018</td>
      </tr>     

      <tr class="content"><!-- 44 -->
         <td class="title"><a href="https://unstats.un.org/sdgs/files/report/2018/TheSustainableDevelopmentGoalsReport2018-EN.pdf">The Sustainable Development Goals Report 2018</a></td>
         <td class="report3">United Nations</td>
         <td>2018</td>
      </tr> 

      <tr class="content"><!-- 45 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/12.pdf">SDGs 연계 성과프레임워크 수립 및 활용방안</a></td>
         <td class="report2">한국국제협력단(KOICA)</td>
         <td>2017</td>
      </tr>

      <tr class="content"><!-- 46 -->
         <td class="title"><a href="https://www.kipa.re.kr/synap/skin/doc.html?fn=FILE_0000000000051891&rs=/convert/result/201512/">지속가능발전목표(SDGs) 이행 실태 분석 및 개선방안 연구</a></td>
         <td class="report2">한국행정연구원</td>
         <td>2017</td>
      </tr>

      <tr class="content"><!-- 47 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/39.pdf">지속가능개발목표(SDGs) 달성을 위한 교육개발협력 연구(Ⅰ) :기초교육 실천 전략</a></td>
         <td class="report2">한국교육개발원</td>
         <td>2017</td>
      </tr>

      <tr class="content"><!-- 48 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/51.pdf">지속가능발전목표(SDGs) 관련, 한국 및 Kwater의 대응전략 연구</a></td>
         <td class="report2">한국수자원공사</td>
         <td>2017</td>
      </tr>

      <tr class="content"><!-- 49 -->
         <td class="title"><a href="https://www.unesco.or.kr/assets/data/report/ELJcHwllZDLUGvi9GpWaCpoMUQveOw__2.pdf">우리의 지속가능한 에너지(SDG 7)</a></td>
         <td class="report2">유네스코한국위원회</td>
         <td>2017</td>
      </tr>


      <tr class="content"><!-- 50 -->
         <td class="title"><a href="https://www.unesco.or.kr/assets/data/report/xNoBXzg8AvKzsQ1zmRL4MCN39Ji3JV__2.pdf">우리의 지속가능한 도시(SDG 11)</a></td>
         <td class="report2">유네스코한국위원회</td>
         <td>2017</td>
      </tr>

      <tr class="content"><!-- 51 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/83.pdf">SDGs 재난지표 측정 연구</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2017</td>
      </tr>     


      <tr class="content"><!-- 52 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/84.pdf">SDGs 통계 거버넌스 연구</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2017</td>
      </tr>

      <tr class="content"><!-- 53 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/87.pdf">통계청 주요 지표체계 간 조정 및 서비스 방안 연구</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2017</td>
      </tr>

      <tr class="content"><!-- 54 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/88.pdf">한국의 주요 지표체계 비교 연구</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2017</td>
      </tr>

      <tr class="content"><!-- 55 -->
         <td class="title"><a href="https://unstats.un.org/sdgs/files/report/2017/TheSustainableDevelopmentGoalsReport2017.pdf">The Sustainable Development Goals Report 2017</a></td>
         <td class="report3">United Nations</td>
         <td>2017</td>
      </tr>

      <tr class="content"><!-- 56 -->
         <td class="title"><a href="https://www.unescap.org/sites/default/files/ESCAP_SYB2016_SDG_baseline_report.pdf">Statistical Yearbook for Asia and the Pacific SDG Progress Report 2016 : SDG Baseline Report</a></td>
         <td class="report3">UN ESCAP</td>
         <td>2017</td>
      </tr>

       <tr class="content"><!-- 57 -->
         <td class="title"><a href="https://www.unescap.org/sites/default/files/publications/Asia-Pacific-SDG-Progress-Report-2017.pdf">Asia and the Pacific SDG Progress Report 2017</a></td>
         <td class="report3">UN ESCAP</td>
         <td>2017</td>

      </tr>
       <tr class="content"><!-- 58 -->
         <td class="title"><a href="https://www.unescap.org/sites/default/files/publications/ASEAN_SDG_Baseline_0.pdf">ASEAN SDG baseline</a></td>
         <td class="report3">UN ESCAP</td>
         <td>2017</td>
      </tr>


      <tr class="content"><!-- 59 -->
         <td class="title"><a href="http://lib.koica.go.kr/search/media/img/CAT000000039786?metsno=000000015736&fileid=M000000015736_FILE000001">알기쉬운 지속가능발전목표 SDGs</a></td>
         <td class="report2">국제개발협력시민사회포럼, 한국국제협력단(KOICA)</td>
         <td>2016</td>
      </tr>

      <tr class="content"><!-- 60 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/26.pdf">UN SDGs 보건·복지분야 지표 관리체계 구축방안 연구</a></td>
         <td class="report2">보건복지부</td>
         <td>2016</td>
      </tr>

      <tr class="content"><!-- 61 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/RR2016-25.pdf">2030 지속가능개발목표(SDGs)실천 방안 연구:교육 분야를 중심으로</a></td>
         <td class="report2">한국교육개발원</td>
         <td>2016</td>
      </tr>
   
      <tr class="content"><!-- 62  -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/45.pdf">여성과 ICT : 지속가능발전목표 5 (양성평등과 여성권익향상)의 이행</a></td>
         <td class="report2">정보통신정책연구원</td>
         <td>2016</td>
      </tr>

      <tr class="content"><!-- 63 -->
         <td class="title"><a href="http://www.klri.re.kr/viewer/skin/doc.html?fn=10%ED%98%B8_%EC%97%AC%EC%84%B1%EC%9D%98%20%EB%85%B8%EB%8F%99%ED%8F%89%EB%93%B1%EA%B6%8C%20%ED%99%95%EB%B3%B4%EB%A5%BC%20%ED%86%B5%ED%95%9C%20%EC%A7%80%EC%86%8D%EA%B0%80%EB%8A%A5%EB%B0%9C%EC%A0%84%EB%AA%A9%ED%91%9C%20%EC%8B%A4%ED%98%84%EA%B3%BC%EC%A0%9C.pdf&rs=/doc_convert/FILE_000000000026094anoOa">여성과 ICT : 지속가능발전목표 5 (양성평등과 여성권익향상)의 이행</a></td>
         <td class="report2">한국법제연구원</td>
         <td>2016</td>
      </tr>


      <tr class="content"><!-- 64 -->
         <td class="title"><a href="https://library.kei.re.kr:444/dmme/img/001/005/014/%eb%ac%bc%eb%b6%84%ec%95%bc%ea%b5%ad%ec%a0%9c%eb%8f%99%ed%96%a5%ea%b3%bc%ed%9a%a8%ec%9c%a8%ec%a0%81%eb%8c%80%ec%9d%91%eb%b0%a9%ec%95%88%ec%97%b0%ea%b5%ac_%ea%b9%80%ed%98%b8%ec%a0%95.pdf">물 분야 국제동향과 효율적 대응방안 연구</a></td>
         <td class="report2">한국환경정책평가연구원</td>
         <td>2016</td>
      </tr>

      <tr class="content"><!-- 65 -->
         <td class="title"><a href="https://library.kei.re.kr:444/dmme/img/001/012/005/%ea%b8%b0%ec%b4%88_2016_11_%eb%aa%85%ec%88%98%ec%a0%95.pdf">토지환경 분야의 지속가능발전목표(SDGs) 이행을 위한 정책 방향</a></td>
         <td class="report2">한국환경정책평가연구원</td>
         <td>2016</td>
      </tr>
      
      <tr class="content"><!-- 66 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/BB2016-784.pdf">SDGs 달성을 위한 중소기업 ODA 정책의 심층 연구</a></td>
         <td class="report2">산업연구원(KIET)</td>
         <td>2016</td>
      </tr>     

      <tr class="content"><!-- 67 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/85.pdf">지속가능발전목표(SDGs) 데이터 세분화와 항목 표준화 연구</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2016</td>
      </tr>

      <tr class="content"><!-- 68 -->
         <td class="title"><a href="https://unstats.un.org/sdgs/report/2016/The%20Sustainable%20Development%20Goals%20Report%202016.pdf">The Sustainable Development Goals Report 2016</a></td>
         <td class="report3">United Nations</td>
         <td>2016</td>
      </tr>

      <tr class="content"><!-- 69 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/openData_SDG.pdf">오픈데이터와 지속가능개발목표(SDG)</a></td>
         <td class="report2">정보통신정책연구원</td>
         <td>2015</td>
      </tr>

      <tr class="content"><!-- 70 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/openData_SDG.pdf">지속가능개발목표(SDGs) 수립현황과 대응방안</a></td>
         <td class="report2">한국국제협력단(KOICA)</td>
         <td>2015</td>
      </tr>

      <tr class="content"><!-- 71 -->
         <td class="title"><a href="https://www.unesco.or.kr/assets/data/report/tqnJNGIqaKI6WDd4MBZSEwWACWWSjC__2.pdf">유네스코 SDG 국제교육협력 포럼 자료집</a></td>
         <td class="report2">유네스코한국위원회</td>
         <td>2015</td>
      </tr>


      <tr class="content"><!-- 72 -->
         <td class="title"><a href="https://library.kei.re.kr:444/dmme/img/001/012/004/%ea%b8%b0%ec%b4%882015_08_%ec%9e%84%ed%98%9c%ec%88%99.pdf">자원순환분야 지속가능발전목표(SDGs) 이행 기반 마련을 위한 기초연구</a></td>
         <td class="report2">한국환경정책평가연구원</td>
         <td>2015</td>
      </tr>

      <tr class="content"><!-- 73 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/86.pdf">2030 지속가능발전의제에 대한 국가통계 대응방안 수립</a></td>
         <td class="report1">통계청 통계개발원</td>
         <td>2015</td>
      </tr>

      <tr class="content"><!-- 74 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/22.pdf">지속가능발전목표(SDGs) 세부대응전략 수립 연구</a></td>
         <td class="report2">한국환경정책평가연구원</td>
         <td>2014</td>
      </tr>
   
      <tr class="content"><!-- 75 -->
         <td class="title"><a href="https://library.kei.re.kr:444/dmme/img/001/009/005/%ea%b8%b0%eb%b3%b82014_21_%ec%a1%b0%ec%9d%84%ec%83%9d.pdf">SDGs 관점의 물인권 지원을 위한 한국의 ODA 전략방향 연구</a></td>
         <td class="report2">한국환경정책평가연구원</td>
         <td>2014</td>
      </tr>

      <tr class="content"><!-- 76 -->
         <td class="title"><a href="https://kostat-sdg-kor.github.io/sdg-indicators/public/report/VNR.pdf">National Voluntary Review Report 2016</a></td>
         <td class="report2">The Government of the Republic of Korea</td>
         <td>2016</td>
      </tr>
      
   </table>
   <div class="page_form">
      <ul class="pagination">
      </ul>
   </div>   
</div>

### Related Sites

－**[IAEG-SDGs(Inter-agency and Expert Group on SDG Indicators)](https://unstats.un.org/sdgs/iaeg-sdgs/)**

－**[UN World Data Forum](https://unstats.un.org/unsd/undataforum/)**

－**[HLPF(High-Level Political Forum)](https://sustainabledevelopment.un.org/hlpf)**

－**[UNESCAP(UN The Economic and Social Commission for Asia and the Pacific)](https://www.unescap.org/)**

－**[UNESCAP-ENEA(UN ESCAP East and North-East Asia Office)](https://www.unescap.org/subregional-office/east-north-east-asia)**

－**[UNECE(UN Economic Commission for Europe)](https://www.unece.org/info/ece-homepage.html)**

－**[UNECA(UN Economic Commission for Africa)](https://www.uneca.org/)**

<br><br>

－**[Germany](http://sdg-indikatoren.de/) : http://sdg-indikatoren.de/**

－**[U.K.](https://sdgdata.gov.uk/) : https://sdgdata.gov.uk/**

－**[U.S.A.](https://sdg.data.gov/) : https://sdg.data.gov/**

－**[Ireland](https://irelandsdg.geohive.ie/) : https://irelandsdg.geohive.ie/**

－**[Poland](https://sdg.gov.pl/) : https://sdg.gov.pl/**

－**[Mexico](http://agenda2030.mx/#/home) : http://agenda2030.mx/#/home**
 

<br/>
<br/>
<br/>
<br/>
<br><br>

