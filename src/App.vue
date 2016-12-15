<template>
    <div style="height:100%;">
      <center>
        <div class="head">
            <p class = "font color">สั่งข้าว Freshy ออนไลน์</p>
        </div>
      </center>
      <br>
      <div v-show = "!adminPage">
        <br><br>
    <div v-show = "newIdUserCheck == 'itkmutnb'">
      <center>
        <div>
          <button class="button is-info font" style = "background-color:#4dd2ff" v-on:click="selectBlueHome()">บ้านฟ้า</button>
          <button class="button is-success font" style = "background-color:#90EE90" v-on:click="selectGreenHome()">บ้านเขียว</button>
          <button class="button is-success font" style = "background-color:#ff944d" v-on:click="selectOrangeHome()">บ้านส้ม</button>
          <button class="button is-success font" style = "background-color:#ffb3d9" v-on:click="selectPinkHome()">บ้านชมพู</button>
        </div>
        </center>
        <br>
        <center>
        <div>
  <a class="button">
    <span class="icon is-small">
      <i class="fa fa-cutlery"></i>
    </span>
    <span class = "font" v-on:click="managerFoods()">เมนูอาหาร</span>
  </a>
  <a class="button">
    <span class="icon is-small">
      <i class="fa fa-pencil"></i>
    </span>
    <span class = "font" v-on:click="addUsers()">จัดการรายชื่อ</span>
  </a>
  <a class="button">
    <span class="icon is-small">
      <i class="fa fa-line-chart"></i>
    </span>
    <span class = "font" v-on:click="countFoods()">ยอดสั่ง</span>
  </a>
        </div>

        <div v-show = "newIdUserCheck == 'itkmutnb' && newIdUserCheck != ''">
          <div v-show="!back" style="text-align : center">
            <br>
            <a class="button is-danger is-outlined">
              <span class = "font" @click = "backFirstPage()">ออกจากระบบ</span>
              <span class="icon">
                <i class="fa fa-reply"></i>
              </span>
            </a>
          </div>
        </div>

        <center>


<div v-show = "!countFoodCheck" style="padding-left: 5%; padding-right: 5%;">
  <hr>
  <div v-for="checkOrders in checkOrder">
  <button class="button font" v-on:click="timeUp(checkOrders.id)">ตัดยอดสั่งข้าว</button>
  <button class="button font" v-on:click="openOder(checkOrders.id)">เปิดสั่งข้าว</button>
  </div>
  <br>
  <div>
    <article class="message is-primary">
      <div class="message-header">
        <center>
        <h2 class = "font">ยอดอาหารเช้า</h2>
        </center>
      </div>
      <div class="message-body">
        <div align="center">
          <div>
            <p class="font" v-for="foodMor in foodsMorning">
                {{foodMor.foodName}}
            </p>
          </div>
        </div>
        <br>
        <div align="center">
          <div class="font">
            {{countFoodBlue.Morning.m1 + countFoodGreen.Morning.m1 + countFoodOrange.Morning.m1 + countFoodPink.Morning.m1}} กล่อง<br>
            {{countFoodBlue.Morning.m2 + countFoodGreen.Morning.m2 + countFoodOrange.Morning.m2 + countFoodPink.Morning.m2}} กล่อง<br>
            {{countFoodBlue.Morning.m3 + countFoodGreen.Morning.m3 + countFoodOrange.Morning.m3 + countFoodPink.Morning.m3}} กล่อง<br>
          </div>
        </div>
        </div>
        </article>
      </div>

      <hr>

      <div>
        <article class="message is-warning">
          <div class="message-header">
            <center>
            <h2 class = "font">ยอดอาหารกลางวัน</h2>
            </center>
          </div>
          <div class="message-body">
            <div align="center">
              <div>
                <p class="font" v-for="foodAfter in foodsAfternoon">
                    {{foodAfter.foodName}}
                </p>
              </div>
            </div>
            <br>
            <div align="center">
              <div class="font">
                {{countFoodBlue.Afternoon.m1  + countFoodGreen.Afternoon.m1 + countFoodOrange.Afternoon.m1 + countFoodPink.Afternoon.m1}} กล่อง<br>
                {{countFoodBlue.Afternoon.m2  + countFoodGreen.Afternoon.m2 + countFoodOrange.Afternoon.m2 + countFoodPink.Afternoon.m2}} กล่อง<br>
                {{countFoodBlue.Afternoon.m3  + countFoodGreen.Afternoon.m3 + countFoodOrange.Afternoon.m3 + countFoodPink.Afternoon.m3}} กล่อง<br>

              </div>
            </div>
            </div>
            </article>
          </div>

      <hr>
      <div>
        <article class="message is-info">
          <div class="message-header">
            <center>
            <h2 class = "font">ยอดอาหารเย็น</h2>
            </center>
          </div>
          <div class="message-body">
            <div align="center">
              <div>
                <p class="font" v-for="foodEve in foodsEvening">
                    {{foodEve.foodName}}
                </p>
              </div>
            </div>
            <br>
            <div align="center">
              <div class="font">
                {{countFoodBlue.Evening.m1  + countFoodGreen.Evening.m1 + countFoodOrange.Evening.m1 + countFoodPink.Evening.m1}} กล่อง<br>
                {{countFoodBlue.Evening.m2  + countFoodGreen.Evening.m2 + countFoodOrange.Evening.m2 + countFoodPink.Evening.m2}} กล่อง<br>
                {{countFoodBlue.Evening.m3  + countFoodGreen.Evening.m3 + countFoodOrange.Evening.m3 + countFoodPink.Evening.m3}} กล่อง<br>
              </div>
            </div>
            </div>
            </article>
          </div>
</div>

<center>
    <div style="padding-left: 4%; padding-right: 1%;" v-show = "homes == '1'" v-for="usersBlue in blueUsers">
    <div style="padding-right: 2%;" v-show = "usersBlue.home == 'บ้านฟ้า'">
      <hr>
                <button class="button is-info font" style = "background-color:#4dd2ff" @click="selectNameBlue(usersBlue.id)">{{usersBlue.name}}</button>
                <button v-show = "(usersBlue.foodMorningName == '' || usersBlue.foodAfternoonName == '' || usersBlue.foodEveningName == '') && usersBlue.temp == true" class="button font" @click="backBlue(usersBlue.id)">ปิดเมนู</button>
                <button class="button is-info font" style="background-color:#FFD700" v-show = "usersBlue.foodMorningName != '' || usersBlue.foodAfternoonName != '' || usersBlue.foodEveningName != ''" @click = "editFoodStaff(usersBlue.id, usersBlue.home)">แก้ไข</button>
                <button class="button is-info font" style="background-color:#FF607F" v-show = "usersBlue.foodMorningName != '' || usersBlue.foodAfternoonName != '' || usersBlue.foodEveningName != ''" @click = "removeFoodsBlue(usersBlue.id)">ลบรายการสั่งข้าว</button>
                <br>
                <div v-show = "usersBlue.foodMorningName != ''">
                  <br>
                  <article class="message">
                    <div class="message-header" style = "background-color:#74828F">
                      <h1 class="font">อาหารเช้า</h1>
                    </div>
                    <div class="message-body">
                  <a class="button font" v-show="usersBlue.foodMorningName != ''">
                  <div>{{usersBlue.foodMorningName}}</div>
                  </a>
                </div>
                </article>
                </div>
                <div v-show = "usersBlue.foodAfternoonName != ''">
                  <br>
                  <article class="message">
                    <div class="message-header" style = "background-color:#74828F">
                      <h1 class="font">อาหารกลางวัน</h1>
                    </div>
                    <div class="message-body">
                  <a class="button font" v-show="usersBlue.foodAfternoonName != ''">
                  <div>{{usersBlue.foodAfternoonName}}</div>
                  </a>
                </div>
                </article>
                </div>
                <div v-show = "usersBlue.foodEveningName != ''">
                  <br>
                  <article class="message">
                    <div class="message-header" style = "background-color:#74828F">
                      <h1 class="font">อาหารเย็น</h1>
                    </div>
                    <div class="message-body">
                  <a class="button font" v-show="usersBlue.foodEveningName != ''">
                  <div>{{usersBlue.foodEveningName}}</div>
                  </a>
                </div>
              </div>
              </article>

                <div v-show = "usersBlue.temp" style="padding-right: 2%; padding-left: 1%;">
                  <br>
                  <article v-show = "usersBlue.foodMorningName == ''" class="message is-primary">
                    <div v-show = "usersBlue.foodMorningName == ''" class="message-header">
                  <h2 class = "font" v-show = "usersBlue.foodMorningName == ''">เมนูอาหารเช้า</h2>
                    </div>
                    <div class="message-body">
                  <div align = "center" v-for="foodMor in foodsMorning" v-show = "usersBlue.foodMorningName == ''">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsMorning(foodMor.foodName, usersBlue.id, usersBlue.home)">{{foodMor.foodName}}</button>
                    </div>
                  </div>
                </article>

                <article v-show = "usersBlue.foodAfternoonName == ''" class="message is-warning">
                  <div v-show = "usersBlue.foodAfternoonName == ''" class="message-header">
                <h2 class = "font" v-show = "usersBlue.foodAfternoonName == ''">เมนูอาหารกลางวัน</h2>
                  </div>
                  <div class="message-body">
                    <div align = "center" v-for="foodAfter in foodsAfternoon" v-show = "usersBlue.foodAfternoonName == ''">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsAfternoon(foodAfter.foodName, usersBlue.id, usersBlue.home)">{{foodAfter.foodName}}</button>
                  </div>
                </div>
              </article>

              <article v-show = "usersBlue.foodEveningName == ''" class="message is-info">
                <div v-show = "usersBlue.foodEveningName == ''" class="message-header">
              <h2 class = "font" v-show = "usersBlue.foodEveningName == ''">เมนูอาหารเย็น</h2>
                </div>
                <div class="message-body">
                    <div align = "center" v-for="foodEve in foodsEvening" v-show = "usersBlue.foodEveningName == ''">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsEvening(foodEve.foodName, usersBlue.id, usersBlue.home)">{{foodEve.foodName}}</button>
                  </div>
                </div>
              </article>
            </div>
            </div>
      </div>

      <div style="padding-left: 4%; padding-right: 1%;" v-show = "homes == '2'" v-for="usersGreen in greenUsers">
      <div style="padding-right: 2%;" v-show = "usersGreen.home == 'บ้านเขียว'">
        <hr>
                  <button class="button is-info font" style = "background-color:#90EE90" @click="selectNameGreen(usersGreen.id)">{{usersGreen.name}}</button>
                  <button v-show = "(usersGreen.foodMorningName == '' || usersGreen.foodAfternoonName == '' || usersGreen.foodEveningName == '') && usersGreen.temp == true" class="button font" @click="backGreen(usersGreen.id)">ปิดเมนู</button>
                  <button class="button is-info font" style="background-color:#FFD700" v-show = "usersGreen.foodMorningName != '' || usersGreen.foodAfternoonName != '' || usersGreen.foodEveningName != ''" @click = "editFoodStaff(usersGreen.id, usersGreen.home)">แก้ไข</button>
                  <button class="button is-info font" style="background-color:#FF607F" v-show = "usersGreen.foodMorningName != '' || usersGreen.foodAfternoonName != '' || usersGreen.foodEveningName != ''" @click = "removeFoodsGreen(usersGreen.id)">ลบรายการสั่งข้าว</button>
                  <br>
                  <div v-show = "usersGreen.foodMorningName != ''">
                    <br>
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารเช้า</h1>
                      </div>
                      <div class="message-body">
                    <a class="button font" v-show="usersGreen.foodMorningName != ''">
                    <div>{{usersGreen.foodMorningName}}</div>
                    </a>
                  </div>
                  </article>
                  </div>
                  <div v-show = "usersGreen.foodAfternoonName != ''">
                    <br>
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารกลางวัน</h1>
                      </div>
                      <div class="message-body">
                    <a class="button font" v-show="usersGreen.foodAfternoonName != ''">
                    <div>{{usersGreen.foodAfternoonName}}</div>
                    </a>
                  </div>
                  </article>
                  </div>
                  <div v-show = "usersGreen.foodEveningName != ''">
                    <br>
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารเย็น</h1>
                      </div>
                      <div class="message-body">
                    <a class="button font" v-show="usersGreen.foodEveningName != ''">
                    <div>{{usersGreen.foodEveningName}}</div>
                    </a>
                  </div>
                  </article>
                  </div>
                  <div v-show = "usersGreen.temp" style = "padding-right: 2%; padding-left: 1%;">
                    <br>
                    <article v-show = "usersGreen.foodMorningName == ''" class="message is-primary">
                      <div v-show = "usersGreen.foodMorningName == ''" class="message-header">
                    <h2 class = "font" v-show = "usersGreen.foodMorningName == ''">เมนูอาหารเช้า</h2>
                      </div>
                      <div class="message-body">
                    <div align = "center" v-for="foodMor in foodsMorning" v-show = "usersGreen.foodMorningName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsMorning(foodMor.foodName, usersGreen.id, usersGreen.home)">{{foodMor.foodName}}</button>
                      </div>
                    </div>
                  </article>

                  <article v-show = "usersGreen.foodAfternoonName == ''" class="message is-warning">
                    <div v-show = "usersGreen.foodAfternoonName == ''" class="message-header">
                  <h2 class = "font" v-show = "usersGreen.foodAfternoonName == ''">เมนูอาหารกลางวัน</h2>
                    </div>
                    <div class="message-body">
                      <div align = "center" v-for="foodAfter in foodsAfternoon" v-show = "usersGreen.foodAfternoonName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsAfternoon(foodAfter.foodName, usersGreen.id, usersGreen.home)">{{foodAfter.foodName}}</button>
                    </div>
                  </div>
                </article>

                <article v-show = "usersGreen.foodEveningName == ''" class="message is-info">
                  <div v-show = "usersGreen.foodEveningName == ''" class="message-header">
                <h2 class = "font" v-show = "usersGreen.foodEveningName == ''">เมนูอาหารเย็น</h2>
                  </div>
                  <div class="message-body">
                      <div align = "center" v-for="foodEve in foodsEvening" v-show = "usersGreen.foodEveningName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsEvening(foodEve.foodName, usersGreen.id, usersGreen.home)">{{foodEve.foodName}}</button>
                    </div>
                  </div>

                </article>
              </div>
              </div>
        </div>

        <div style="padding-left: 4%; padding-right: 1%;" v-show = "homes == '3'" v-for="usersOrange in orangeUsers">
        <div style="padding-right: 2%;" v-show = "usersOrange.home == 'บ้านส้ม'">
          <hr>
                    <button class="button is-info font" style = "background-color:#ff944d" @click="selectNameOrange(usersOrange.id)">{{usersOrange.name}}</button>
                    <button v-show = "(usersOrange.foodMorningName == '' || usersOrange.foodAfternoonName == '' || usersOrange.foodEveningName == '') && usersOrange.temp == true" class="button is-danger font" style = "background-color:#ffGreen6666" @click="backOrange(usersOrange.id)">ปิดเมนู</button>
                    <button class="button is-info font" style = "background-color:#FFD700" v-show = "usersOrange.foodMorningName != '' || usersOrange.foodAfternoonName != '' || usersOrange.foodEveningName != ''" @click = "editFoodStaff(usersOrange.id, usersOrange.home)">แก้ไข</button>
                    <button class="button is-info font" style = "background-color:#FF607F" v-show = "usersOrange.foodMorningName != '' || usersOrange.foodAfternoonName != '' || usersOrange.foodEveningName != ''" @click = "removeFoodsOrange(usersOrange.id)">ลบรายการสั่งข้าว</button>
                    <br>
                    <div v-show = "usersOrange.foodMorningName != ''">
                      <br>
                      <article class="message">
                        <div class="message-header" style = "background-color:#74828F">
                          <h1 class="font">อาหารเช้า</h1>
                        </div>
                        <div class="message-body">
                      <a class="button font" v-show="usersOrange.foodMorningName != ''">
                      <div>{{usersOrange.foodMorningName}}</div>
                      </a>
                    </div>
                  </article>
                    </div>
                    <div v-show = "usersOrange.foodAfternoonName != ''">
                      <br>
                      <article class="message">
                        <div class="message-header" style = "background-color:#74828F">
                          <h1 class="font">อาหารกลางวัน</h1>
                        </div>
                        <div class="message-body">
                      <a class="button font" v-show="usersOrange.foodAfternoonName != ''">
                      <div>{{usersOrange.foodAfternoonName}}</div>
                      </a>
                    </div>
                  </article>
                    </div>
                    <div v-show = "usersOrange.foodEveningName != ''">
                      <br>
                      <article class="message">
                        <div class="message-header" style = "background-color:#74828F">
                          <h1 class="font">อาหารเย็น</h1>
                        </div>
                        <div class="message-body">
                      <a class="button font" v-show="usersOrange.foodEveningName != ''">
                      <div>{{usersOrange.foodEveningName}}</div>
                      </a>
                    </div>
                  </article>
                    </div>
                    <div v-show = "usersOrange.temp" style = "padding-right: 2%; padding-left: 1%;">
                      <br>
                      <article v-show = "usersOrange.foodMorningName == ''" class="message is-primary">
                        <div v-show = "usersOrange.foodMorningName == ''" class="message-header">
                      <h2 class = "font" v-show = "usersOrange.foodMorningName == ''">เมนูอาหารเช้า</h2>
                        </div>
                        <div class="message-body">
                      <div align = "center" v-for="foodMor in foodsMorning" v-show = "usersOrange.foodMorningName == ''">
                        <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsMorning(foodMor.foodName, usersOrange.id, usersOrange.home)">{{foodMor.foodName}}</button>
                        </div>
                      </div>
                    </article>

                    <article v-show = "usersOrange.foodAfternoonName == ''" class="message is-warning">
                      <div v-show = "usersOrange.foodAfternoonName == ''" class="message-header">
                    <h2 class = "font" v-show = "usersOrange.foodAfternoonName == ''">เมนูอาหารกลางวัน</h2>
                      </div>
                      <div class="message-body">
                        <div align = "center" v-for="foodAfter in foodsAfternoon" v-show = "usersOrange.foodAfternoonName == ''">
                        <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsAfternoon(foodAfter.foodName, usersOrange.id, usersOrange.home)">{{foodAfter.foodName}}</button>
                      </div>
                    </div>
                  </article>

                  <article v-show = "usersOrange.foodEveningName == ''" class="message is-info">
                    <div v-show = "usersOrange.foodEveningName == ''" class="message-header">
                  <h2 class = "font" v-show = "usersOrange.foodEveningName == ''">เมนูอาหารเย็น</h2>
                    </div>
                    <div class="message-body">
                        <div align = "center" v-for="foodEve in foodsEvening" v-show = "usersOrange.foodEveningName == ''">
                        <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsEvening(foodEve.foodName, usersOrange.id, usersOrange.home)">{{foodEve.foodName}}</button>
                      </div>
                    </div>

                  </article>
                </div>
                </div>
          </div>

          <div style="padding-left: 4%; padding-right: 1%;" v-show = "homes == '4'" v-for="usersPink in pinkUsers">
          <div style="padding-right: 2%;" v-show = "usersPink.home == 'บ้านชมพู'">
            <hr>
                      <button class="button is-info font" style = "background-color:#ffb3d9" @click="selectNamePink(usersPink.id)">{{usersPink.name}}</button>
                      <button v-show = "(usersPink.foodMorningName == '' || usersPink.foodAfternoonName == '' || usersPink.foodEveningName == '') && usersPink.temp == true" class="button is-danger font" style = "background-color:#ffGreen6666" @click="backPink(usersPink.id)">ปิดเมนู</button>
                      <button class="button is-info font" style = "background-color:#FFD700" v-show = "usersPink.foodMorningName != '' || usersPink.foodAfternoonName != '' || usersPink.foodEveningName != ''" @click = "editFoodStaff(usersPink.id, usersPink.home)">แก้ไข</button>
                      <button class="button is-info font" style = "background-color:#FF607F" v-show = "usersPink.foodMorningName != '' || usersPink.foodAfternoonName != '' || usersPink.foodEveningName != ''" @click = "removeFoodsPink(usersPink.id)">ลบรายการสั่งข้าว</button>
                      <br>
                      <div v-show = "usersPink.foodMorningName != ''">
                        <br>
                        <article class="message">
                          <div class="message-header" style = "background-color:#74828F">
                            <h1 class="font">อาหารเช้า</h1>
                          </div>
                          <div class="message-body">
                        <a class="button font" v-show="usersPink.foodMorningName != ''">
                        <div>{{usersPink.foodMorningName}}</div>
                        </a>
                      </div>
                    </article>
                      </div>
                      <div v-show = "usersPink.foodAfternoonName != ''">
                        <br>
                        <article class="message">
                          <div class="message-header" style = "background-color:#74828F">
                            <h1 class="font">อาหารกลางวัน</h1>
                          </div>
                          <div class="message-body">
                        <a class="button font" v-show="usersPink.foodAfternoonName != ''">
                        <div>{{usersPink.foodAfternoonName}}</div>
                        </a>
                      </div>
                    </article>
                      </div>
                      <div v-show = "usersPink.foodEveningName != ''">
                        <br>
                        <article class="message">
                          <div class="message-header" style = "background-color:#74828F">
                            <h1 class="font">อาหารเย็น</h1>
                          </div>
                          <div class="message-body">
                        <a class="button font" v-show="usersPink.foodEveningName != ''">
                        <div>{{usersPink.foodEveningName}}</div>
                        </a>
                      </div>
                    </article>
                      </div>
                      <div v-show = "usersPink.temp" style = "padding-right: 2%; padding-left: 1%;">
                        <br>
                        <article v-show = "usersPink.foodMorningName == ''" class="message is-primary">
                          <div v-show = "usersPink.foodMorningName == ''" class="message-header">
                        <h2 class = "font" v-show = "usersPink.foodMorningName == ''">เมนูอาหารเช้า</h2>
                          </div>
                          <div class="message-body">
                        <div align = "center" v-for="foodMor in foodsMorning" v-show = "usersPink.foodMorningName == ''">
                          <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsMorning(foodMor.foodName, usersPink.id, usersPink.home)">{{foodMor.foodName}}</button>
                          </div>
                        </div>
                      </article>

                      <article v-show = "usersPink.foodAfternoonName == ''" class="message is-warning">
                        <div v-show = "usersPink.foodAfternoonName == ''" class="message-header">
                      <h2 class = "font" v-show = "usersPink.foodAfternoonName == ''">เมนูอาหารกลางวัน</h2>
                        </div>
                        <div class="message-body">
                          <div align = "center" v-for="foodAfter in foodsAfternoon" v-show = "usersPink.foodAfternoonName == ''">
                          <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsAfternoon(foodAfter.foodName, usersPink.id, usersPink.home)">{{foodAfter.foodName}}</button>
                        </div>
                      </div>
                    </article>

                    <article v-show = "usersPink.foodEveningName == ''" class="message is-info">
                      <div v-show = "usersPink.foodEveningName == ''" class="message-header">
                    <h2 class = "font" v-show = "usersPink.foodEveningName == ''">เมนูอาหารเย็น</h2>
                      </div>
                      <div class="message-body">
                          <div align = "center" v-for="foodEve in foodsEvening" v-show = "usersPink.foodEveningName == ''">
                          <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsEvening(foodEve.foodName, usersPink.id, usersPink.home)">{{foodEve.foodName}}</button>
                        </div>
                      </div>

                    </article>
                  </div>
                  </div>
            </div>
    </center>


    <div v-show = "!statusManage" style="padding-left: 5%; padding-right: 5%;">
      <hr>
      <article class="message is-primary">
        <div class="message-header">
          <center>
      <h2 class = "font">เมนูอาหารเช้า</h2>
    </center>
        </div>
        <div class="message-body">
      <div align = "center" v-for="foodMor in foodsMorning">
    <button align = "center" class="button font" style="width:120px;">{{foodMor.foodName}}</button>
    <button class="button is-danger is-outlined font" v-on:click="removeFoodsMorning(foodMor)">X</button>
  </div>
  </div>
  </article>
  <div style="padding-left: 15%;" class = "font">
  <p class="control has-addons">
    <input type="text" v-model="newFoodMorning.foodName" class="input font" placeholder="เมนูอาหารเช้า">
    <button @click = "addFoodsMorning()" class="button font">
      เพิ่ม
    </button>
  </p>
  </div>

    <hr>

    <article class="message is-warning">
      <div class="message-header">
        <center>
    <h2 class = "font">เมนูอาหารกลางวัน</h2>
  </center>
      </div>
      <div class="message-body">
    <div align = "center" v-for="foodAfter in foodsAfternoon">
  <button align = "center" class="button font" style="width:120px;">{{foodAfter.foodName}}</button>
  <button class="button is-danger is-outlined font" v-on:click="removeFoodsAfternoon(foodAfter)">X</button>
</div>
</div>
</article>
<div style="padding-left: 15%;" class = "font">
<p class="control has-addons">
  <input type="text" v-model="newFoodAfternoon.foodName" class="input font" placeholder="เมนูอาหารกลางวัน">
  <button @click = "addFoodsAfternoon()" class="button font">
    เพิ่ม
  </button>
</p>
</div>
    <hr>
    <article class="message is-info">
      <div class="message-header">
        <center>
    <h2 class = "font">เมนูอาหารเย็น</h2>
  </center>
      </div>
      <div class="message-body">
    <div align = "center" v-for="foodEve in foodsEvening">
    <button align = "center" class="button font" style="width:120px;">{{foodEve.foodName}}</button>
    <button class="button is-danger is-outlined font" v-on:click="removeFoodsEvening(foodEve)">X</button>
    </div>
    </div>
    </article>
    <div style="padding-left: 15%;" class = "font">
    <p class="control has-addons">
    <input type="text" v-model="newFoodEvening.foodName" class="input font" placeholder="เมนูอาหารเย็น">
    <button @click = "addFoodsEvening()" class="button font">
    เพิ่ม
    </button>
    </p>
    </div>
    </div>

    <div v-show ="!statusUsers">

    <center>
      <hr>
      <div v-show = "show">
        <button v-show = "showPlusBlue" class="button is-info font" style = "background-color:#4dd2ff" @click = "blueHomeChecks()">เพิ่มรายชื่อบ้านฟ้า</button>
        <button v-show = "showRemoveBlue" class="button is-info font" style = "background-color:#4dd2ff" @click = "blueHomeRemove()">ลบรายชื่อบ้านฟ้า</button>
        <br><br>
        <button v-show = "showPlusGreen" class="button is-success font" style = "background-color:#90EE90" @click = "greenHomeChecks()">เพิ่มรายชื่อบ้านเขียว</button>
        <button v-show = "showRemoveGreen" class="button is-success font" style = "background-color:#90EE90" @click = "greenHomeRemove()">ลบรายชื่อบ้านเขียว</button>
        <br><br>
        <button v-show = "showPlusOrange" class="button is-success font" style = "background-color:#ff944d" @click = "orangeHomeChecks()">เพิ่มรายชื่อบ้านส้ม</button>
        <button v-show = "showRemoveOrange" class="button is-success font" style = "background-color:#ff944d" @click = "orangeHomeRemove()">ลบรายชื่อบ้านส้ม</button>
        <br><br>
        <button v-show = "showPlusPink" class="button is-success font" style = "background-color:#ffb3d9" @click = "pinkHomeChecks()">เพิ่มรายชื่อบ้านชมพู</button>
        <button v-show = "showRemovePink" class="button is-success font" style = "background-color:#ffb3d9" @click = "pinkHomeRemove()">ลบรายชื่อบ้านชมพู</button>
      </div>
  </center>
    <div v-show = "checkInBlue">
    <div v-show = "blueHomeCheck">

    <div>
      <div align="center">
        <button class="button is-info font" style = "background-color:#4dd2ff">เพิ่มรายชื่อบ้านฟ้า</button>
      </div>
      <br>
    <center>
      <div style="padding-left: 30%; padding-right: 30%;">
    <input type="text" v-model="newBlueUsers.name" class="input font" placeholder="ชื่อ">
    </div>
    </center>
    <center>
      <br>
      <div style="padding-left: 30%; padding-right: 30%;">
    <input type="number" v-model="newBlueUsers.idUser" class="input font" placeholder="รหัสนักศึกษา">
    </div>
    </center>
    <center>
      <br>
      <div style="padding-left: 30%; padding-right: 30%;">
    <input type="text" v-model="newBlueUsers.idCard" class="input font" placeholder="วันเกิด">
    </div>
    <p class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
    </center>
    <center>
      <div style="margin-top: 3%; margin-bottom: 7%;">
        <a class="button is-success" v-show = "newBlueUsers.name != '' && newBlueUsers.idUser != '' && newBlueUsers.idCard != ''">
  <span class="icon">
    <i class="fa fa-check"></i>
  </span>
  <span v-show = "newBlueUsers.name != '' && newBlueUsers.idUser != ''" @click="addBlueUsers()">เพิ่ม</span>
</a>
<a class="button is-danger">
  <span class="icon">
    <i class="fa fa-times"></i>
  </span>
  <span v-show = "blueHomeCheck" @click ="blueHomeBacks()">ยกเลิก</span>
</a>
      </div>
    </center>
  </div>

    </div>
    </div>

    <div v-show = "checkInGreen">
    <div v-show = "greenHomeCheck">

    <div>
      <div align="center">
        <button class="button is-info font" style = "background-color:#90EE90">เพิ่มรายชื่อบ้านเขียว</button>
      </div>
      <br>
    <center>
      <div style="padding-left: 30%; padding-right: 30%;">
    <input type="text" v-model="newGreenUsers.name" class="input font" placeholder="ชื่อ">
    </div>
    </center>
    <center>
      <br>
      <div style="padding-left: 30%; padding-right: 30%;">
    <input type="number" v-model="newGreenUsers.idUser" class="input font" placeholder="รหัสนักศึกษา">
    </div>
    </center>
    <center>
      <br>
      <div style="padding-left: 30%; padding-right: 30%;">
    <input type="text" v-model="newGreenUsers.idCard" class="input font" placeholder="วันเกิด">
    </div>
    <p class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
    </center>
    <center>
      <div style="margin-top: 3%; margin-bottom: 7%;">
        <a class="button is-success" v-show = "newGreenUsers.name != '' && newGreenUsers.idUser != '' && newGreenUsers.idCard != ''">
  <span class="icon">
    <i class="fa fa-check"></i>
  </span>
  <span v-show = "newGreenUsers.name != '' && newGreenUsers.idUser != ''" @click="addGreenUsers()">เพิ่ม</span>
</a>
<a class="button is-danger">
  <span class="icon">
    <i class="fa fa-times"></i>
  </span>
  <span v-show = "greenHomeCheck" @click ="greenHomeBacks()">ยกเลิก</span>
</a>
      </div>
    </center>
  </div>

    </div>
    </div>

    <div v-show = "checkInOrange">
    <div v-show = "orangeHomeCheck">

    <div>
      <div align="center">
        <button class="button is-info font" style = "background-color:#ff944d">เพิ่มรายชื่อบ้านส้ม</button>
      </div>
      <br>
    <center>
      <div style="padding-left: 30%; padding-right: 30%;">
    <input type="text" v-model="newOrangeUsers.name" class="input font" placeholder="ชื่อ">
    </div>
    </center>
    <center>
      <br>
      <div style="padding-left: 30%; padding-right: 30%;">
    <input type="number" v-model="newOrangeUsers.idUser" class="input font" placeholder="รหัสนักศึกษา">
    </div>
    </center>
    <center>
      <br>
      <div style="padding-left: 30%; padding-right: 30%;">
    <input type="text" v-model="newOrangeUsers.idCard" class="input font" placeholder="วันเกิด">
    </div>
    <p class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
    </center>
    <center>
      <div style="margin-top: 3%; margin-bottom: 7%;">
        <a class="button is-success" v-show = "newOrangeUsers.name != '' && newOrangeUsers.idUser != '' && newOrangeUsers.idCard != ''">
  <span class="icon">
    <i class="fa fa-check"></i>
  </span>
  <span v-show = "newOrangeUsers.name != '' && newOrangeUsers.idUser != ''" @click="addOrangeUsers()">เพิ่ม</span>
</a>
<a class="button is-danger">
  <span class="icon">
    <i class="fa fa-times"></i>
  </span>
  <span v-show = "orangeHomeCheck" @click ="orangeHomeBacks()">ยกเลิก</span>
</a>
      </div>
    </center>
  </div>

    </div>
    </div>

    <div v-show = "checkInPink">
    <div v-show = "pinkHomeCheck">

    <div>
      <div align="center">
        <button class="button is-info font" style = "background-color:#ffb3d9">เพิ่มรายชื่อบ้านชมพู</button>
      </div>
      <br>
    <center>
      <div style="padding-left: 30%; padding-right: 30%;">
    <input type="text" v-model="newPinkUsers.name" class="input font" placeholder="ชื่อ">
    </div>
    </center>
    <center>
      <br>
      <div style="padding-left: 30%; padding-right: 30%;">
    <input type="number" v-model="newPinkUsers.idUser" class="input font" placeholder="รหัสนักศึกษา">
    </div>
    </center>
    <center>
      <br>
      <div style="padding-left: 30%; padding-right: 30%;">
    <input type="text" v-model="newPinkUsers.idCard" class="input font" placeholder="วันเกิด">
    </div>
    <p class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
    </center>
    <center>
      <div style="margin-top: 3%; margin-bottom: 7%;">
        <a class="button is-success" v-show = "newPinkUsers.name != '' && newPinkUsers.idUser != '' && newPinkUsers.idCard != ''">
  <span class="icon">
    <i class="fa fa-check"></i>
  </span>
  <span v-show = "newPinkUsers.name != '' && newPinkUsers.idUser != ''" @click="addPinkUsers()">เพิ่ม</span>
</a>
<a class="button is-danger">
  <span class="icon">
    <i class="fa fa-times"></i>
  </span>
  <span v-show = "pinkHomeCheck" @click ="pinkHomeBacks()">ยกเลิก</span>
</a>
      </div>
    </center>
  </div>

    </div>
    </div>
    </div>

    <div v-show = "blueHomeRemoveCheck">

    <div>
      <div align="center" style="margin-bottom: 5%;">
        <button class="button is-info font" style = "background-color:#4dd2ff">ลบชื่อบ้านฟ้า</button>
      </div>
    <center>
      <div v-for="usersBlue in blueUsers">
        <a class="button font">
        {{usersBlue.name}}
        </a>
        <a @click="deleteBlueUser(usersBlue)" class="button is-danger is-outlined">ลบ</a>
        <br><br>
      </div>
    </center>
  </div>

    </div>

    <div v-show = "greenHomeRemoveCheck">

    <div>
      <div align="center" style="margin-bottom: 5%;">
        <button class="button is-info font" style = "background-color:#90EE90">ลบชื่อบ้านเขียว</button>
      </div>
    <center>
      <div v-for="usersGreen in greenUsers">
        <a class="button font">
        {{usersGreen.name}}
        </a>
        <a @click="deleteGreenUser(usersGreen)" class="button is-danger is-outlined">ลบ</a>
        <br><br>
      </div>
    </center>
  </div>

    </div>

    <div v-show = "orangeHomeRemoveCheck">

    <div>
      <div align="center" style="margin-bottom: 5%;">
        <button class="button is-info font" style = "background-color:#ff944d">ลบชื่อบ้านส้ม</button>
      </div>
    <center>
      <div v-for="usersOrange in orangeUsers">
        <a class="button font">
        {{usersOrange.name}}
        </a>
        <a @click="deleteOrangeUser(usersOrange)" class="button is-danger is-outlined">ลบ</a>
        <br><br>
      </div>
    </center>
  </div>

    </div>

    <div v-show = "pinkHomeRemoveCheck">

    <div>
      <div align="center" style="margin-bottom: 5%;">
        <button class="button is-info font" style = "background-color:#ffb3d9">ลบชื่อบ้านชมพู</button>
      </div>
    <center>
      <div v-for="usersPink in pinkUsers">
        <a class="button font">
        {{usersPink.name}}
        </a>
        <a @click="deletePinkUser(usersPink)" class="button is-danger is-outlined">ลบ</a>
        <br><br>
      </div>
    </center>
  </div>

    </div>
<hr>
</div>

  </div>
    <div v-show = "guestPage">
      <br><br>
      <div style="padding-left: 10%; padding-right: 5%;" class="font">
        <label  class="label">เข้าสู่ระบบ</label>
        <p class="control has-addons control has-icon font">
          <i class="fa fa-envelope"></i>
          <input v-model="newIdUser" class="input font" placeholder="รหัสนักศึกษา">
          <button @click = "search(newIdUser)" class="button font">
            ตกลง
          </button>
        </p>
      </div>
      <center>

        <div style="padding-left: 4%; padding-right: 1%;">
              <div v-for="usersBlue in blueUsers" style="padding-right: 2%;">
                <div v-show = "usersBlue.idUser == newIdUserCheck && usersBlue.idUser != ''">
                  <br>
                  <div v-show = "ei && (usersBlue.foodMorningName == '' && usersBlue.foodAfternoonName == '' && usersBlue.foodEveningName == '')">
                    <div v-for="checkOrders in checkOrder">
                      <p v-show = "checkOrders.order == true">
                    <button class="button is-info font" style = "background-color:#4dd2ff" @click="selectNameBlue(usersBlue.id)">{{usersBlue.name}}</button>
                    <p v-show = "checkOrders.order == true" style="margin-top: 1%;" class="font">(คลิ๊กที่ชื่อ)</p>
                    <p v-show = "checkOrders.order == false" style="margin-top: 1%;" class="font">ไม่สามารถสั่งข้าวได้ เนื่องจากปิดรอบการสั่งแล้ว</p>
                  </p>
                  <br>
                  </div>
                  </div>
                  <div v-for="checkOrders in checkOrder">
                  <button v-show = "ei2 || (usersBlue.foodMorningName != '' || usersBlue.foodAfternoonName != '' || usersBlue.foodEveningName != '')" class="button is-info font" style = "background-color:#4dd2ff">{{usersBlue.name}}</button>
                  <a v-show="usersBlue.foodMorningName != '' || usersBlue.foodAfternoonName != '' || usersBlue.foodEveningName != ''">
                  <button class="button font" v-show = "checkOrders.order && showOpen && (usersBlue.foodMorningName == '' || usersBlue.foodAfternoonName == '' || usersBlue.foodEveningName == '')" @click = "openFoodsBlueUser(usersBlue.id)">เปิดเมนู</button>
                  </a>
                  <button v-show = "(usersBlue.foodMorningName == '' || usersBlue.foodAfternoonName == '' || usersBlue.foodEveningName == '') && checkShowMenuBlue == true" class="button font" @click="backBlue(usersBlue.id)">ปิดเมนู</button>
                  <button class="button is-info font" style="background-color:#FF607F" v-show = "(usersBlue.foodMorningName != '' || usersBlue.foodAfternoonName != '' || usersBlue.foodEveningName != '') && checkOrders.order == true" @click = "removeFoodsBlueUser()">ลบรายการสั่งข้าว</button>
                </p>
              </div>
                  <div v-show = "!clickNameBlue">
                    <center>
                      <br>
                      <p class="font">ใส่วันเกิดเพื่อยืนยันตัวตน</p>
                      <div style="padding-left: 30%; padding-right: 30%;">
                    <input v-show = "!showEditButton" type="password" v-model="newBlueUsers.idCard" class="input font" placeholder="วันเกิด">
                    <input v-show = "showEditButton2" type="password" v-model="newBlueUsers.idCard" class="input font" placeholder="วันเกิด">
                    </div>
                    <p v-show = "!showEditButton" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <p v-show = "showEditButton2" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <button v-show = "!showEditButton" @click = "checkClickBlue(usersBlue.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "!showEditButton" @click = "cancleClickNameBlue(usersBlue.id)" class="button font">
                      ยกเลิก
                    </button>
                    <br><br>
                    <button v-show = "showEditButton2" @click = "editFood(usersBlue.id, usersBlue.idCard)" class="button font">
                      ตกลง
                    </button>
                    </center>
                  </div>

                  <div v-show = "!submitEditFoodMor">
                    <center>
                      <br>
                      <p class="font">ใส่วันเกิดเพื่อยืนยันตัวตน</p>
                      <div style="padding-left: 30%; padding-right: 30%;">
                    <input v-show = "showEditButton3" type="password" v-model="newBlueUsers.idCard" class="input font" placeholder="วันเกิด">
                    </div>
                    <p v-show = "showEditButton3" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <button v-show = "showEditButton3 && !buttonEditMor" @click = "editFoodMorSuccess(usersBlue.id, usersBlue.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditMor" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditAfter" @click = "editFoodAfterSuccess(usersBlue.id, usersBlue.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditAfter" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditEve" @click = "editFoodEveSuccess(usersBlue.id, usersBlue.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditEve" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveMor" @click = "removeFoodMorSuccess(usersBlue.id, usersBlue.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveMor" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveAfter" @click = "removeFoodAfterSuccess(usersBlue.id, usersBlue.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveAfter" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveEve" @click = "removeFoodEveSuccess(usersBlue.id, usersBlue.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveEve" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonAdd" @click = "addFoodSuccess(usersBlue.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonAdd" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    </center>
                  </div>

                  <div v-show = "!deleteFoodMor">
                    <center>
                      <br>
                      <p class="font">ใส่วันเกิดเพื่อยืนยันตัวตน</p>
                      <div style="padding-left: 30%; padding-right: 30%;">
                    <input v-show = "showEditButton4" type="password" v-model="newBlueUsers.idCard" class="input font" placeholder="วันเกิด">
                    </div>
                    <p v-show = "showEditButton4" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <button v-show = "showEditButton4" @click = "deleteFoodBlueMorSuccess(usersBlue.id, usersBlue.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton4" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    </center>
                  </div>
                  <br>
                  <div v-show = "editMorBlueTwo" v-for="checkOrders in checkOrder">
                  <div v-show = "usersBlue.foodMorningName != ''">
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารเช้า</h1>
                      </div>
                      <div class="message-body">
                    <a class="button is-white font" v-show="usersBlue.foodMorningName != ''">
                    <div>{{usersBlue.foodMorningName}}</div>
                    </a>
                    <button class="button font" v-show = "usersBlue.foodMorningName != '' && checkOrders.order == true" @click = "editMorBlue()">แก้ไข</button>
                    <button class="button font" v-show = "usersBlue.foodMorningName != '' && checkOrders.order == true" @click="cancleFoodMor()">ยกเลิกเมนู</button>
                    <br>
                  </div>
                </div>
              </article>
                </div>

                <div v-show = "editAfterBlueTwo" v-for="checkOrders in checkOrder">
                  <div v-show = "usersBlue.foodAfternoonName != ''">
                    <br>
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารกลางวัน</h1>
                      </div>
                      <div class="message-body">
                    <a class="button is-white font" v-show="usersBlue.foodAfternoonName != ''">
                    <div>{{usersBlue.foodAfternoonName}}</div>
                    </a>
                    <button class="button font" v-show = "usersBlue.foodAfterName != '' && checkOrders.order == true" @click = "editAfterBlue()">แก้ไข</button>
                    <button class="button font" v-show = "usersBlue.foodAfterName != '' && checkOrders.order == true" @click="cancleFoodAfter()">ยกเลิกเมนู</button>
                    <br>
                  </div>
                </div>
              </article>
                </div>

                <div v-show = "editEveBlueTwo" v-for="checkOrders in checkOrder">
                  <div v-show = "usersBlue.foodEveningName != ''">
                    <br>
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารเย็น</h1>
                      </div>
                      <div class="message-body">
                    <a class="button is-white font" v-show="usersBlue.foodEveningName != ''">
                    <div>{{usersBlue.foodEveningName}}</div>
                    </a>
                    <button class="button font" v-show = "usersBlue.foodEveName != '' && checkOrders.order == true" @click = "editEveBlue()">แก้ไข</button>
                    <button class="button font" v-show = "usersBlue.foodEveName != '' && checkOrders.order == true" @click="cancleFoodEve()">ยกเลิกเมนู</button>
                    <br>
                  </div>
                  <br>
                </div>
              </article>
                </div>

                  <div v-show = "checkShowMenuBlue" style="padding-right: 1%;">
                    <br>
                    <article v-show = "usersBlue.foodMorningName == ''" class="message is-primary">
                      <div v-show = "usersBlue.foodMorningName == ''" class="message-header">
                    <h2 class = "font" v-show = "usersBlue.foodMorningName == ''">เมนูอาหารเช้า</h2>
                      </div>
                      <div class="message-body">
                    <div align = "center" v-for="foodMor in foodsMorning" v-show = "usersBlue.foodMorningName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsMorning(foodMor.foodName, usersBlue.id, usersBlue.home)">{{foodMor.foodName}}</button>
                      </div>
                    </div>
                  </article>

                  <article v-show = "usersBlue.foodAfternoonName == ''" class="message is-warning">
                    <div v-show = "usersBlue.foodAfternoonName == ''" class="message-header">
                  <h2 class = "font" v-show = "usersBlue.foodAfternoonName == ''">เมนูอาหารกลางวัน</h2>
                    </div>
                    <div class="message-body">
                      <div align = "center" v-for="foodAfter in foodsAfternoon" v-show = "usersBlue.foodAfternoonName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsAfternoon(foodAfter.foodName, usersBlue.id, usersBlue.home)">{{foodAfter.foodName}}</button>
                    </div>
                  </div>
                </article>

                <article v-show = "usersBlue.foodEveningName == ''" class="message is-info">
                  <div v-show = "usersBlue.foodEveningName == ''" class="message-header">
                <h2 class = "font" v-show = "usersBlue.foodEveningName == ''">เมนูอาหารเย็น</h2>
                  </div>
                  <div class="message-body">
                      <div align = "center" v-for="foodEve in foodsEvening" v-show = "usersBlue.foodEveningName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsEvening(foodEve.foodName, usersBlue.id, usersBlue.home)">{{foodEve.foodName}}</button>
                    </div>
                </div>
                <br>
                </article>
                </div>

                <div v-show = "!editMorBlueTwo">
                  <br>
                  <article class="message is-primary">
                    <div class="message-header">
                  <h2 class = "font">เมนูอาหารเช้า</h2>
                    </div>
                    <div class="message-body">
                  <div align = "center" v-for="foodMor in foodsMorning">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsMorning(foodMor.foodName, usersBlue.id, usersBlue.home)">{{foodMor.foodName}}</button>
                    </div>
                  </div>
                </article>
                <button class="button font" @click="cancleEdit()">ยกเลิกแก้ไข</button>
                <br><br>
                </div>

                <div v-show = "!editAfterBlueTwo">
                  <br>
                  <article class="message is-warning">
                    <div class="message-header">
                  <h2 class = "font">เมนูอาหารกลางวัน</h2>
                    </div>
                    <div class="message-body">
                  <div align = "center" v-for="foodAfter in foodsAfternoon">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsAfternoon(foodAfter.foodName, usersBlue.id, usersBlue.home)">{{foodAfter.foodName}}</button>
                    </div>
                  </div>
                </article>
                <button class="button font" @click="cancleEdit()">ยกเลิกแก้ไข</button>
                <br><br>
                </div>

                <div v-show = "!editEveBlueTwo">
                  <br>
                  <article class="message is-info">
                    <div class="message-header">
                  <h2 class = "font">เมนูอาหารเย็น</h2>
                    </div>
                    <div class="message-body">
                  <div align = "center" v-for="foodEve in foodsEvening">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsEvening(foodEve.foodName, usersBlue.id, usersBlue.home)">{{foodEve.foodName}}</button>
                    </div>
                  </div>
                </article>
                <button class="button font" @click="cancleEdit()">ยกเลิกแก้ไข</button>
                <br><br>
                </div>


                </div>
              </div>
        </div>

        <div style="padding-left: 4%; padding-right: 1%;">
              <div v-for="usersGreen in greenUsers" style="padding-right: 2%;">
                <div v-show = "usersGreen.idUser == newIdUserCheck && usersGreen.idUser != ''">
                  <br>
                  <div v-show = "ei && (usersGreen.foodMorningName == '' && usersGreen.foodAfternoonName == '' && usersGreen.foodEveningName == '')">
                    <div v-for="checkOrders in checkOrder">
                      <p v-show = "checkOrders.order == true">
                    <button class="button is-info font" style = "background-color:#90EE90" @click="selectNameGreen(usersGreen.id)">{{usersGreen.name}}</button>
                    <p v-show = "checkOrders.order == true" style="margin-top: 1%;" class="font">(คลิ๊กที่ชื่อ)</p>
                    <p v-show = "checkOrders.order == false" style="margin-top: 1%;" class="font">ไม่สามารถสั่งข้าวได้ เนื่องจากปิดรอบการสั่งแล้ว</p>
                  </p>
                  <br>
                  </div>
                  </div>
                  <div v-for="checkOrders in checkOrder">
                  <button v-show = "ei2 || (usersGreen.foodMorningName != '' || usersGreen.foodAfternoonName != '' || usersGreen.foodEveningName != '')" class="button is-info font" style = "background-color:#90EE90">{{usersGreen.name}}</button>
                  <a v-show="usersGreen.foodMorningName != '' || usersGreen.foodAfternoonName != '' || usersGreen.foodEveningName != ''">
                  <button class="button font" v-show = "checkOrders.order && showOpen && (usersGreen.foodMorningName == '' || usersGreen.foodAfternoonName == '' || usersGreen.foodEveningName == '')" @click = "openFoodsGreenUser(usersGreen.id)">เปิดเมนู</button>
                  </a>
                  <button v-show = "(usersGreen.foodMorningName == '' || usersGreen.foodAfternoonName == '' || usersGreen.foodEveningName == '') && checkShowMenuGreen == true" class="button font" @click="backGreen(usersGreen.id)">ปิดเมนู</button>
                  <button class="button is-danger font" style="background-color:#FF607F" v-show = "(usersGreen.foodMorningName != '' || usersGreen.foodAfternoonName != '' || usersGreen.foodEveningName != '') && checkOrders.order == true" @click = "removeFoodsGreenUser()">ลบรายการสั่งข้าว</button>
                </div>
                  <div v-show = "!clickNameGreen">
                    <center>
                      <br>
                      <p class="font">ใส่วันเกิดเพื่อยืนยันตัวตน</p>
                      <div style="padding-left: 30%; padding-right: 30%;">
                    <input v-show = "!showEditButton" type="password" v-model="newGreenUsers.idCard" class="input font" placeholder="วันเกิด">
                    <input v-show = "showEditButton2" type="password" v-model="newGreenUsers.idCard" class="input font" placeholder="วันเกิด">
                    </div>
                    <p v-show = "!showEditButton" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <p v-show = "showEditButton2" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <button v-show = "!showEditButton" @click = "checkClickGreen(usersGreen.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "!showEditButton" @click = "cancleClickNameGreen()" class="button font">
                      ยกเลิก
                    </button>
                    <br><br>
                    <button v-show = "showEditButton2" @click = "editFood(usersGreen.id, usersGreen.idCard)" class="button font">
                      ตกลง
                    </button>
                    </center>
                  </div>

                  <div v-show = "!submitEditFoodMor">
                    <center>
                      <br>
                      <p class="font">ใส่วันเกิดเพื่อยืนยันตัวตน</p>
                      <div style="padding-left: 30%; padding-right: 30%;">
                    <input v-show = "showEditButton3" type="password" v-model="newGreenUsers.idCard" class="input font" placeholder="วันเกิด">
                    </div>
                    <p v-show = "showEditButton3" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <button v-show = "showEditButton3 && !buttonEditMor" @click = "editFoodMorSuccess(usersGreen.id, usersGreen.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditMor" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditAfter" @click = "editFoodAfterSuccess(usersGreen.id, usersGreen.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditAfter" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditEve" @click = "editFoodEveSuccess(usersGreen.id, usersGreen.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditEve" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveMor" @click = "removeFoodMorSuccess(usersGreen.id, usersGreen.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveMor" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveAfter" @click = "removeFoodAfterSuccess(usersGreen.id, usersGreen.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveAfter" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveEve" @click = "removeFoodEveSuccess(usersGreen.id, usersGreen.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveEve" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonAdd" @click = "addFoodSuccess(usersGreen.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonAdd" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    </center>
                  </div>

                  <div v-show = "!deleteFoodMor">
                    <center>
                      <br>
                      <p class="font">ใส่วันเกิดเพื่อยืนยันตัวตน</p>
                      <div style="padding-left: 30%; padding-right: 30%;">
                    <input v-show = "showEditButton4" type="password" v-model="newGreenUsers.idCard" class="input font" placeholder="วันเกิด">
                    </div>
                    <p v-show = "showEditButton4" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <button v-show = "showEditButton4" @click = "deleteFoodGreenMorSuccess(usersGreen.id, usersGreen.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton4" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    </center>
                  </div>
                  <br>
                  <div v-show = "editMorGreenTwo" v-for="checkOrders in checkOrder">
                  <div v-show = "usersGreen.foodMorningName != ''">
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารเช้า</h1>
                      </div>
                      <div class="message-body">
                    <a class="button is-white font" v-show="usersGreen.foodMorningName != ''">
                    <div>{{usersGreen.foodMorningName}}</div>
                    </a>
                    <button class="button font" v-show = "usersGreen.foodMorningName != '' && checkOrders.order == true" @click = "editMorGreen()">แก้ไข</button>
                    <button class="button font" v-show = "usersGreen.foodMorningName != '' && checkOrders.order == true" @click="cancleFoodMor()">ยกเลิกเมนู</button>
                    <br>
                  </div>
                </div>
              </article>
                </div>

                <div v-show = "editAfterGreenTwo" v-for="checkOrders in checkOrder">
                  <div v-show = "usersGreen.foodAfternoonName != ''">
                    <br>
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารกลางวัน</h1>
                      </div>
                      <div class="message-body">
                    <a class="button is-white font" v-show="usersGreen.foodAfternoonName != ''">
                    <div>{{usersGreen.foodAfternoonName}}</div>
                    </a>
                    <button class="button font" v-show = "usersGreen.foodAfterName != '' && checkOrders.order == true" @click = "editAfterGreen()">แก้ไข</button>
                    <button class="button font" v-show = "usersGreen.foodAfterName != '' && checkOrders.order == true" @click="cancleFoodAfter()">ยกเลิกเมนู</button>
                    <br>
                  </div>
                </div>
              </article>
                </div>

                <div v-show = "editEveGreenTwo" v-for="checkOrders in checkOrder">
                  <div v-show = "usersGreen.foodEveningName != ''">
                    <br>
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารเย็น</h1>
                      </div>
                      <div class="message-body">
                    <a class="button is-white font" v-show="usersGreen.foodEveningName != ''">
                    <div>{{usersGreen.foodEveningName}}</div>
                    </a>
                    <button class="button font" v-show = "usersGreen.foodEveName != '' && checkOrders.order == true" @click = "editEveGreen()">แก้ไข</button>
                    <button class="button font" v-show = "usersGreen.foodEveName != '' && checkOrders.order == true" @click="cancleFoodEve()">ยกเลิกเมนู</button>
                    <br>
                  </div>
                  <br>
                </div>
              </article>
                </div>

                  <div v-show = "checkShowMenuGreen" style="padding-right: 1%;">
                    <br>
                    <article v-show = "usersGreen.foodMorningName == ''" class="message is-primary">
                      <div v-show = "usersGreen.foodMorningName == ''" class="message-header">
                    <h2 class = "font" v-show = "usersGreen.foodMorningName == ''">เมนูอาหารเช้า</h2>
                      </div>
                      <div class="message-body">
                    <div align = "center" v-for="foodMor in foodsMorning" v-show = "usersGreen.foodMorningName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsMorning(foodMor.foodName, usersGreen.id, usersGreen.home)">{{foodMor.foodName}}</button>
                      </div>
                    <div>
                  </article>

                  <article v-show = "usersGreen.foodAfternoonName == ''" class="message is-warning">
                    <div v-show = "usersGreen.foodAfternoonName == ''" class="message-header">
                  <h2 class = "font" v-show = "usersGreen.foodAfternoonName == ''">เมนูอาหารกลางวัน</h2>
                    </div>
                    <div class="message-body">
                      <div align = "center" v-for="foodAfter in foodsAfternoon" v-show = "usersGreen.foodAfternoonName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsAfternoon(foodAfter.foodName, usersGreen.id, usersGreen.home)">{{foodAfter.foodName}}</button>
                    </div>
                </div>
                </article>

                <article v-show = "usersGreen.foodEveningName == ''" class="message is-info">
                  <div v-show = "usersGreen.foodEveningName == ''" class="message-header">
                <h2 class = "font" v-show = "usersGreen.foodEveningName == ''">เมนูอาหารเย็น</h2>
                  </div>
                  <div class="message-body">
                      <div align = "center" v-for="foodEve in foodsEvening" v-show = "usersGreen.foodEveningName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsEvening(foodEve.foodName, usersGreen.id, usersGreen.home)">{{foodEve.foodName}}</button>
                    </div>
                </div>
                <br>
                </article>
                </div>

                <div v-show = "!editMorGreenTwo">
                  <br>
                  <article class="message is-primary">
                    <div class="message-header">
                  <h2 class = "font">เมนูอาหารเช้า</h2>
                    </div>
                    <div class="message-body">
                  <div align = "center" v-for="foodMor in foodsMorning">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsMorning(foodMor.foodName, usersGreen.id, usersGreen.home)">{{foodMor.foodName}}</button>
                    </div>
                  </div>
                </article>
                <button class="button font" @click="cancleEdit()">ยกเลิกแก้ไข</button>
                <br><br>
                </div>

                <div v-show = "!editAfterGreenTwo">
                  <br>
                  <article class="message is-warning">
                    <div class="message-header">
                  <h2 class = "font">เมนูอาหารกลางวัน</h2>
                    </div>
                    <div class="message-body">
                  <div align = "center" v-for="foodAfter in foodsAfternoon">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsAfternoon(foodAfter.foodName, usersGreen.id, usersGreen.home)">{{foodAfter.foodName}}</button>
                    </div>
                  </div>
                </article>
                <button class="button font" @click="cancleEdit()">ยกเลิกแก้ไข</button>
                <br><br>
                </div>

                <div v-show = "!editEveGreenTwo">
                  <br>
                  <article class="message is-info">
                    <div class="message-header">
                  <h2 class = "font">เมนูอาหารเย็น</h2>
                    </div>
                    <div class="message-body">
                  <div align = "center" v-for="foodEve in foodsEvening">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsEvening(foodEve.foodName, usersGreen.id, usersGreen.home)">{{foodEve.foodName}}</button>
                    </div>
                  </div>
                </article>
                <button class="button font" @click="cancleEdit()">ยกเลิกแก้ไข</button>
                <br><br>
                </div>


                </div>
              </div>
        </div>

        <div style="padding-left: 4%; padding-right: 1%;">
              <div v-for="usersOrange in orangeUsers" style="padding-right: 2%;">
                <div v-show = "usersOrange.idUser == newIdUserCheck && usersOrange.idUser != ''">
                  <br>
                  <div v-show = "ei && (usersOrange.foodMorningName == '' && usersOrange.foodAfternoonName == '' && usersOrange.foodEveningName == '')">
                    <div v-for="checkOrders in checkOrder">
                      <p v-show = "checkOrders.order == true">
                    <button class="button is-info font" style = "background-color:#ff944d" @click="selectNameOrange(usersOrange.id)">{{usersOrange.name}}</button>
                    <p v-show = "checkOrders.order == true" style="margin-top: 1%;" class="font">(คลิ๊กที่ชื่อ)</p>
                    <p v-show = "checkOrders.order == false" style="margin-top: 1%;" class="font">ไม่สามารถสั่งข้าวได้ เนื่องจากปิดรอบการสั่งแล้ว</p>
                  </p>
                  <br>
                  </div>
                  </div>
                  <div v-for="checkOrders in checkOrder">
                  <button v-show = "ei2 || (usersOrange.foodMorningName != '' || usersOrange.foodAfternoonName != '' || usersOrange.foodEveningName != '')" class="button is-info font" style = "background-color:#ff944d">{{usersOrange.name}}</button>
                  <a v-show="usersOrange.foodMorningName != '' || usersOrange.foodAfternoonName != '' || usersOrange.foodEveningName != ''">
                  <button class="button font" v-show = "checkOrders.order && showOpen && (usersOrange.foodMorningName == '' || usersOrange.foodAfternoonName == '' || usersOrange.foodEveningName == '')" @click = "openFoodsOrangeUser(usersOrange.id)">เปิดเมนู</button>
                  </a>
                  <button v-show = "(usersOrange.foodMorningName == '' || usersOrange.foodAfternoonName == '' || usersOrange.foodEveningName == '') && checkShowMenuOrange == true" class="button font" @click="backOrange(usersOrange.id)">ปิดเมนู</button>
                  <button class="button is-info font" style="background-color:#FF607F" v-show = "(usersOrange.foodMorningName != '' || usersOrange.foodAfternoonName != '' || usersOrange.foodEveningName != '') && checkOrders.order == true" @click = "removeFoodsOrangeUser()">ลบรายการสั่งข้าว</button>
              </div>
                  <div v-show = "!clickNameOrange">
                    <center>
                      <br>
                      <p class="font">ใส่วันเกิดเพื่อยืนยันตัวตน</p>
                      <div style="padding-left: 30%; padding-right: 30%;">
                    <input v-show = "!showEditButton" type="password" v-model="newOrangeUsers.idCard" class="input font" placeholder="วันเกิด">
                    <input v-show = "showEditButton2" type="password" v-model="newOrangeUsers.idCard" class="input font" placeholder="วันเกิด">
                    </div>
                    <p v-show = "!showEditButton" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <p v-show = "showEditButton2" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <button v-show = "!showEditButton" @click = "checkClickOrange(usersOrange.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "!showEditButton" @click = "cancleClickNameOrange()" class="button font">
                      ยกเลิก
                    </button>
                    <br><br>
                    <button v-show = "showEditButton2" @click = "editFood(usersOrange.id, usersOrange.idCard)" class="button font">
                      ตกลง
                    </button>
                    </center>
                  </div>

                  <div v-show = "!submitEditFoodMor">
                    <center>
                      <br>
                      <p class="font">ใส่วันเกิดเพื่อยืนยันตัวตน</p>
                      <div style="padding-left: 30%; padding-right: 30%;">
                    <input v-show = "showEditButton3" type="password" v-model="newOrangeUsers.idCard" class="input font" placeholder="วันเกิด">
                    </div>
                    <p v-show = "showEditButton3" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <button v-show = "showEditButton3 && !buttonEditMor" @click = "editFoodMorSuccess(usersOrange.id, usersOrange.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditMor" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditAfter" @click = "editFoodAfterSuccess(usersOrange.id, usersOrange.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditAfter" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditEve" @click = "editFoodEveSuccess(usersOrange.id, usersOrange.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditEve" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveMor" @click = "removeFoodMorSuccess(usersOrange.id, usersOrange.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveMor" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveAfter" @click = "removeFoodAfterSuccess(usersOrange.id, usersOrange.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveAfter" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveEve" @click = "removeFoodEveSuccess(usersOrange.id, usersOrange.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveEve" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonAdd" @click = "addFoodSuccess(usersOrange.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonAdd" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    </center>
                  </div>

                  <div v-show = "!deleteFoodMor">
                    <center>
                      <br>
                      <p class="font">ใส่วันเกิดเพื่อยืนยันตัวตน</p>
                      <div style="padding-left: 30%; padding-right: 30%;">
                    <input v-show = "showEditButton4" type="password" v-model="newOrangeUsers.idCard" class="input font" placeholder="วันเกิด">
                    </div>
                    <p v-show = "showEditButton4" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <button v-show = "showEditButton4" @click = "deleteFoodOrangeMorSuccess(usersOrange.id, usersOrange.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton4" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    </center>
                  </div>

                  <br>
                  <div v-show = "editMorOrangeTwo" v-for="checkOrders in checkOrder">
                  <div v-show = "usersOrange.foodMorningName != ''">
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารเช้า</h1>
                      </div>
                      <div class="message-body">
                    <a class="button is-white font" v-show="usersOrange.foodMorningName != ''">
                    <div>{{usersOrange.foodMorningName}}</div>
                    </a>
                    <button class="button font" v-show = "usersOrange.foodMorningName != '' && checkOrders.order == true" @click = "editMorOrange()">แก้ไข</button>
                    <button class="button font" v-show = "usersOrange.foodMorningName != '' && checkOrders.order == true" @click="cancleFoodMor()">ยกเลิกเมนู</button>
                    <br>
                  </div>
                </div>
              </article>
                </div>

                <div v-show = "editAfterOrangeTwo" v-for="checkOrders in checkOrder">
                  <div v-show = "usersOrange.foodAfternoonName != ''">
                    <br>
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารกลางวัน</h1>
                      </div>
                      <div class="message-body">
                    <a class="button is-white font" v-show="usersOrange.foodAfternoonName != ''">
                    <div>{{usersOrange.foodAfternoonName}}</div>
                    </a>
                    <button class="button font" v-show = "usersOrange.foodAfterName != '' && checkOrders.order == true" @click = "editAfterOrange()">แก้ไข</button>
                    <button class="button font" v-show = "usersOrange.foodAfterName != '' && checkOrders.order == true" @click="cancleFoodAfter()">ยกเลิกเมนู</button>
                    <br>
                  </div>
                </div>
              </article>
                </div>

                <div v-show = "editEveOrangeTwo" v-for="checkOrders in checkOrder">
                  <div v-show = "usersOrange.foodEveningName != ''">
                    <br>
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารเย็น</h1>
                      </div>
                      <div class="message-body">
                    <a class="button is-white font" v-show="usersOrange.foodEveningName != ''">
                    <div>{{usersOrange.foodEveningName}}</div>
                    </a>
                    <button class="button font" v-show = "usersOrange.foodEveName != '' && checkOrders.order == true" @click = "editEveOrange()">แก้ไข</button>
                    <button class="button font" v-show = "usersOrange.foodEveName != '' && checkOrders.order == true" @click="cancleFoodEve()">ยกเลิกเมนู</button>
                    <br>
                  </div>
                  <br>
                </div>
              </article>
                </div>

                  <div v-show = "checkShowMenuOrange" style="padding-right: 1%;">
                    <br>
                    <article v-show = "usersOrange.foodMorningName == ''" class="message is-primary">
                      <div v-show = "usersOrange.foodMorningName == ''" class="message-header">
                    <h2 class = "font" v-show = "usersOrange.foodMorningName == ''">เมนูอาหารเช้า</h2>
                      </div>
                      <div class="message-body">
                    <div align = "center" v-for="foodMor in foodsMorning" v-show = "usersOrange.foodMorningName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsMorning(foodMor.foodName, usersOrange.id, usersOrange.home)">{{foodMor.foodName}}</button>
                      </div>
                  </div>
                  </article>

                  <article v-show = "usersOrange.foodAfternoonName == ''" class="message is-warning">
                    <div v-show = "usersOrange.foodAfternoonName == ''" class="message-header">
                  <h2 class = "font" v-show = "usersOrange.foodAfternoonName == ''">เมนูอาหารกลางวัน</h2>
                    </div>
                    <div class="message-body">
                      <div align = "center" v-for="foodAfter in foodsAfternoon" v-show = "usersOrange.foodAfternoonName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsAfternoon(foodAfter.foodName, usersOrange.id, usersOrange.home)">{{foodAfter.foodName}}</button>
                    </div>
                  </div>
                </article>

                <article v-show = "usersOrange.foodEveningName == ''" class="message is-info">
                  <div v-show = "usersOrange.foodEveningName == ''" class="message-header">
                <h2 class = "font" v-show = "usersOrange.foodEveningName == ''">เมนูอาหารเย็น</h2>
                  </div>
                  <div class="message-body">
                      <div align = "center" v-for="foodEve in foodsEvening" v-show = "usersOrange.foodEveningName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsEvening(foodEve.foodName, usersOrange.id, usersOrange.home)">{{foodEve.foodName}}</button>
                    </div>
                </div>
                <br>
                </article>
                </div>

                <div v-show = "!editMorOrangeTwo">
                  <br>
                  <article class="message is-primary">
                    <div class="message-header">
                  <h2 class = "font">เมนูอาหารเช้า</h2>
                    </div>
                    <div class="message-body">
                  <div align = "center" v-for="foodMor in foodsMorning">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsMorning(foodMor.foodName, usersOrange.id, usersOrange.home)">{{foodMor.foodName}}</button>
                    </div>
                  </div>
                </article>
                <button class="button font" @click="cancleEdit()">ยกเลิกแก้ไข</button>
                <br><br>
                </div>

                <div v-show = "!editAfterOrangeTwo">
                  <br>
                  <article class="message is-warning">
                    <div class="message-header">
                  <h2 class = "font">เมนูอาหารกลางวัน</h2>
                    </div>
                    <div class="message-body">
                  <div align = "center" v-for="foodAfter in foodsAfternoon">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsAfternoon(foodAfter.foodName, usersOrange.id, usersOrange.home)">{{foodAfter.foodName}}</button>
                    </div>
                  </div>
                </article>
                <button class="button font" @click="cancleEdit()">ยกเลิกแก้ไข</button>
                <br><br>
                </div>

                <div v-show = "!editEveOrangeTwo">
                  <br>
                  <article class="message is-info">
                    <div class="message-header">
                  <h2 class = "font">เมนูอาหารเย็น</h2>
                    </div>
                    <div class="message-body">
                  <div align = "center" v-for="foodEve in foodsEvening">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsEvening(foodEve.foodName, usersOrange.id, usersOrange.home)">{{foodEve.foodName}}</button>
                    </div>
                  </div>
                </article>
                <button class="button font" @click="cancleEdit()">ยกเลิกแก้ไข</button>
                <br><br>
                </div>


                </div>
              </div>
        </div>


        <div style="padding-left: 4%; padding-right: 1%;">
              <div v-for="usersPink in pinkUsers" style="padding-right: 2%;">
                <div v-show = "usersPink.idUser == newIdUserCheck && usersPink.idUser != ''">
                  <br>
                  <div v-show = "ei && (usersPink.foodMorningName == '' && usersPink.foodAfternoonName == '' && usersPink.foodEveningName == '')">
                    <div v-for="checkOrders in checkOrder">
                      <p v-show = "checkOrders.order == true">
                    <button class="button is-info font" style = "background-color:#ffb3d9" @click="selectNamePink(usersPink.id)">{{usersPink.name}}</button>
                    <p v-show = "checkOrders.order == true" style="margin-top: 1%;" class="font">(คลิ๊กที่ชื่อ)</p>
                    <p v-show = "checkOrders.order == false" style="margin-top: 1%;" class="font">ไม่สามารถสั่งข้าวได้ เนื่องจากปิดรอบการสั่งแล้ว</p>
                  </p>
                  <br>
                  </div>
                  </div>
                  <div v-for="checkOrders in checkOrder">
                  <button v-show = "ei2 || (usersPink.foodMorningName != '' || usersPink.foodAfternoonName != '' || usersPink.foodEveningName != '')" class="button is-info font" style = "background-color:#ffb3d9">{{usersPink.name}}</button>
                  <a v-show="usersPink.foodMorningName != '' || usersPink.foodAfternoonName != '' || usersPink.foodEveningName != ''">
                  <button class="button font" v-show = "checkOrders.order && showOpen && (usersPink.foodMorningName == '' || usersPink.foodAfternoonName == '' || usersPink.foodEveningName == '')" @click = "openFoodsPinkUser(usersPink.id)">เปิดเมนู</button>
                  </a>
                  <button v-show = "(usersPink.foodMorningName == '' || usersPink.foodAfternoonName == '' || usersPink.foodEveningName == '') && checkShowMenuPink == true" class="button font" @click="backPink(usersPink.id)">ปิดเมนู</button>
                  <button class="button is-info font" style="background-color:#FF607F" v-show = "(usersPink.foodMorningName != '' || usersPink.foodAfternoonName != '' || usersPink.foodEveningName != '') && checkOrders.order == true" @click = "removeFoodsPinkUser()">ลบรายการสั่งข้าว</button>
              </div>
                  <div v-show = "!clickNamePink">
                    <center>
                      <br>
                      <p class="font">ใส่วันเกิดเพื่อยืนยันตัวตน</p>
                      <div style="padding-left: 30%; padding-right: 30%;">
                    <input v-show = "!showEditButton" type="password" v-model="newPinkUsers.idCard" class="input font" placeholder="วันเกิด">
                    <input v-show = "showEditButton2" type="password" v-model="newPinkUsers.idCard" class="input font" placeholder="วันเกิด">
                    </div>
                    <p v-show = "!showEditButton" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <p v-show = "showEditButton2" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <button v-show = "!showEditButton" @click = "checkClickPink(usersPink.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "!showEditButton" @click = "cancleClickNamePink()" class="button font">
                      ยกเลิก
                    </button>
                    <br><br>
                    <button v-show = "showEditButton2" @click = "editFood(usersPink.id, usersPink.idCard)" class="button font">
                      ตกลง
                    </button>
                    </center>
                  </div>

                  <div v-show = "!submitEditFoodMor">
                    <center>
                      <br>
                      <p class="font">ใส่วันเกิดเพื่อยืนยันตัวตน</p>
                      <div style="padding-left: 30%; padding-right: 30%;">
                    <input v-show = "showEditButton3" type="password" v-model="newPinkUsers.idCard" class="input font" placeholder="วันเกิด">
                    </div>
                    <p v-show = "showEditButton3" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <button v-show = "showEditButton3 && !buttonEditMor" @click = "editFoodMorSuccess(usersPink.id, usersPink.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditMor" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditAfter" @click = "editFoodAfterSuccess(usersPink.id, usersPink.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditAfter" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditEve" @click = "editFoodEveSuccess(usersPink.id, usersPink.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonEditEve" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveMor" @click = "removeFoodMorSuccess(usersPink.id, usersPink.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveMor" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveAfter" @click = "removeFoodAfterSuccess(usersPink.id, usersPink.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveAfter" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveEve" @click = "removeFoodEveSuccess(usersPink.id, usersPink.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonRemoveEve" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    <button v-show = "showEditButton3 && !buttonAdd" @click = "addFoodSuccess(usersPink.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton3 && !buttonAdd" @click = "removeEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    </center>
                  </div>

                  <div v-show = "!deleteFoodMor">
                    <center>
                      <br>
                      <p class="font">ใส่วันเกิดเพื่อยืนยันตัวตน</p>
                      <div style="padding-left: 30%; padding-right: 30%;">
                    <input v-show = "showEditButton4" type="password" v-model="newPinkUsers.idCard" class="input font" placeholder="วันเกิด">
                    </div>
                    <p v-show = "showEditButton4" class="font">ตัวอย่าง (1 มกราคม 2259 = 010159)</p>
                    <button v-show = "showEditButton4" @click = "deleteFoodPinkMorSuccess(usersPink.id, usersPink.idCard)" class="button font">
                      ตกลง
                    </button>
                    <button v-show = "showEditButton4" @click = "cancleEditPass()" class="button font">
                      ยกเลิก
                    </button>
                    </center>
                  </div>

                  <br>
                  <div v-show = "editMorPinkTwo" v-for="checkOrders in checkOrder">
                  <div v-show = "usersPink.foodMorningName != ''">
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารเช้า</h1>
                      </div>
                      <div class="message-body">
                    <a class="button is-white font" v-show="usersPink.foodMorningName != ''">
                    <div>{{usersPink.foodMorningName}}</div>
                    </a>
                    <button class="button font" v-show = "usersPink.foodMorningName != '' && checkOrders.order == true" @click = "editMorPink()">แก้ไข</button>
                    <button class="button font" v-show = "usersPink.foodMorningName != '' && checkOrders.order == true" @click="cancleFoodMor()">ยกเลิกเมนู</button>
                    <br>
                  </div>
                </div>
              </article>
                </div>

                <div v-show = "editAfterPinkTwo" v-for="checkOrders in checkOrder">
                  <div v-show = "usersPink.foodAfternoonName != ''">
                    <br>
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารกลางวัน</h1>
                      </div>
                      <div class="message-body">
                    <a class="button is-white font" v-show="usersPink.foodAfternoonName != ''">
                    <div>{{usersPink.foodAfternoonName}}</div>
                    </a>
                    <button class="button font" v-show = "usersPink.foodAfterName != '' && checkOrders.order == true" @click = "editAfterPink()">แก้ไข</button>
                    <button class="button font" v-show = "usersPink.foodAfterName != '' && checkOrders.order == true" @click="cancleFoodAfter()">ยกเลิกเมนู</button>
                    <br>
                  </div>
                </div>
              </article>
                </div>

                <div v-show = "editEvePinkTwo" v-for="checkOrders in checkOrder">
                  <div v-show = "usersPink.foodEveningName != ''">
                    <br>
                    <article class="message">
                      <div class="message-header" style = "background-color:#74828F">
                        <h1 class="font">อาหารเย็น</h1>
                      </div>
                      <div class="message-body">
                    <a class="button is-white font" v-show="usersPink.foodEveningName != ''">
                    <div>{{usersPink.foodEveningName}}</div>
                    </a>
                    <button class="button font" v-show = "usersPink.foodEveName != '' && checkOrders.order == true" @click = "editEvePink()">แก้ไข</button>
                    <button class="button font" v-show = "usersPink.foodEveName != '' && checkOrders.order == true" @click="cancleFoodEve()">ยกเลิกเมนู</button>
                    <br>
                  </div>
                  <br>
                </div>
              </article>
                </div>

                  <div v-show = "checkShowMenuPink" style="padding-right: 1%;">
                    <br>
                    <article v-show = "usersPink.foodMorningName == ''" class="message is-primary">
                      <div v-show = "usersPink.foodMorningName == ''" class="message-header">
                    <h2 class = "font" v-show = "usersPink.foodMorningName == ''">เมนูอาหารเช้า</h2>
                      </div>
                      <div class="message-body">
                    <div align = "center" v-for="foodMor in foodsMorning" v-show = "usersPink.foodMorningName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsMorning(foodMor.foodName, usersPink.id, usersPink.home)">{{foodMor.foodName}}</button>
                      </div>
                    </div>
                  </article>

                  <article v-show = "usersPink.foodAfternoonName == ''" class="message is-warning">
                    <div v-show = "usersPink.foodAfternoonName == ''" class="message-header">
                  <h2 class = "font" v-show = "usersPink.foodAfternoonName == ''">เมนูอาหารกลางวัน</h2>
                    </div>
                    <div class="message-body">
                      <div align = "center" v-for="foodAfter in foodsAfternoon" v-show = "usersPink.foodAfternoonName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsAfternoon(foodAfter.foodName, usersPink.id, usersPink.home)">{{foodAfter.foodName}}</button>
                    </div>
                  </div>
                </article>

                <article v-show = "usersPink.foodEveningName == ''" class="message is-info">
                  <div v-show = "usersPink.foodEveningName == ''" class="message-header">
                <h2 class = "font" v-show = "usersPink.foodEveningName == ''">เมนูอาหารเย็น</h2>
                  </div>
                  <div class="message-body">
                      <div align = "center" v-for="foodEve in foodsEvening" v-show = "usersPink.foodEveningName == ''">
                      <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsEvening(foodEve.foodName, usersPink.id, usersPink.home)">{{foodEve.foodName}}</button>
                    </div>
                  </div>
                  <br>
                </article>
                </div>

                <div v-show = "!editMorPinkTwo">
                  <br>
                  <article class="message is-primary">
                    <div class="message-header">
                  <h2 class = "font">เมนูอาหารเช้า</h2>
                    </div>
                    <div class="message-body">
                  <div align = "center" v-for="foodMor in foodsMorning">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsMorning(foodMor.foodName, usersPink.id, usersPink.home)">{{foodMor.foodName}}</button>
                    </div>
                  </div>
                </article>
                <button class="button font" @click="cancleEdit()">ยกเลิกแก้ไข</button>
                <br><br>
                </div>

                <div v-show = "!editAfterPinkTwo">
                  <br>
                  <article class="message is-warning">
                    <div class="message-header">
                  <h2 class = "font">เมนูอาหารกลางวัน</h2>
                    </div>
                    <div class="message-body">
                  <div align = "center" v-for="foodAfter in foodsAfternoon">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsAfternoon(foodAfter.foodName, usersPink.id, usersPink.home)">{{foodAfter.foodName}}</button>
                    </div>
                  </div>
                </article>
                <button class="button font" @click="cancleEdit()">ยกเลิกแก้ไข</button>
                <br><br>
                </div>

                <div v-show = "!editEvePinkTwo">
                  <br>
                  <article class="message is-info">
                    <div class="message-header">
                  <h2 class = "font">เมนูอาหารเย็น</h2>
                    </div>
                    <div class="message-body">
                  <div align = "center" v-for="foodEve in foodsEvening">
                    <button align = "center" class="button font" style="width:120px;" @click = "selectFoodsEvening(foodEve.foodName, usersPink.id, usersPink.home)">{{foodEve.foodName}}</button>
                    </div>
                  </div>
                </article>
                <button class="button font" @click="cancleEdit()">ยกเลิกแก้ไข</button>
                <br><br>
                </div>


                </div>
              </div>
        </div>





</center>
  </div>
<div v-for ="usersBlue in blueUsers">
  <div v-show = "usersBlue.idUser == newIdUserCheck && usersBlue.idUser != ''">
    <div v-show="!back" style="text-align : center">
      <a class="button is-danger is-outlined">
        <span class = "font" @click = "backFirstPage()">ออกจากระบบ</span>
        <span class="icon">
          <i class="fa fa-reply"></i>
        </span>
      </a>
    </div>
  </div>
</div>
<div v-for ="usersGreen in greenUsers">
  <div v-show = "usersGreen.idUser == newIdUserCheck && usersGreen.idUser != ''">
    <div v-show="!back" style="text-align : center">
      <a class="button is-danger is-outlined">
        <span class = "font" @click = "backFirstPage()">ออกจากระบบ</span>
        <span class="icon">
          <i class="fa fa-reply"></i>
        </span>
      </a>
    </div>
  </div>
</div>
<div v-for ="usersOrange in orangeUsers">
  <div v-show = "usersOrange.idUser == newIdUserCheck && usersOrange.idUser != ''">
    <div v-show="!back" style="text-align : center">
      <a class="button is-danger is-outlined">
        <span class = "font" @click = "backFirstPage()">ออกจากระบบ</span>
        <span class="icon">
          <i class="fa fa-reply"></i>
        </span>
      </a>
    </div>
  </div>
</div>
<div v-for ="usersPink in pinkUsers">
  <div v-show = "usersPink.idUser == newIdUserCheck && usersPink.idUser != ''">
    <div v-show="!back" style="text-align : center">
      <a class="button is-danger is-outlined">
        <span class = "font" @click = "backFirstPage()">ออกจากระบบ</span>
        <span class="icon">
          <i class="fa fa-reply"></i>
        </span>
      </a>
    </div>
  </div>
</div>

<br>
</div>
</template>

<script>
/* global swal */
import firebase from 'firebase'
var config = {
  piKey: 'AIzaSyDc17wzlunSiPPGW5UKoKCiacU7veqG1ao',
  authDomain: 'foodsorderit.firebaseapp.com',
  databaseURL: 'https://foodsorderit.firebaseio.com',
  storageBucket: 'foodsorderit.appspot.com',
  messagingSenderId: '394818710035'
}
firebase.initializeApp(config)
var foodsMorning = firebase.database().ref('foodsMorning')
var foodsAfternoon = firebase.database().ref('foodsAfternoon')
var foodsEvening = firebase.database().ref('foodsEvening')
var blueUsers = firebase.database().ref('blueUsers')
var greenUsers = firebase.database().ref('greenUsers')
var orangeUsers = firebase.database().ref('orangeUsers')
var pinkUsers = firebase.database().ref('pinkUsers')
var checkOrder = firebase.database().ref('checkOrder')
export default {
  mounted () {
    let vm = this
    foodsMorning.on('child_added', function (snapshot) {
      var itemMor = snapshot.val()
      itemMor.id = snapshot.key
      vm.foodsMorning.push(itemMor)
    })
    foodsMorning.on('child_removed', function (snapshot) {
      var idMor = snapshot.key
      vm.foodsMorning.splice(vm.foodsMorning.findIndex(foodMor => foodMor.id === idMor), 1)
    })
    let va = this
    foodsAfternoon.on('child_added', function (snapshot) {
      var itemAfter = snapshot.val()
      itemAfter.id = snapshot.key
      va.foodsAfternoon.push(itemAfter)
    })
    foodsAfternoon.on('child_removed', function (snapshot) {
      var idAfter = snapshot.key
      va.foodsAfternoon.splice(va.foodsAfternoon.findIndex(foodAfter => foodAfter.id === idAfter), 1)
    })
    let ve = this
    foodsEvening.on('child_added', function (snapshot) {
      var itemEve = snapshot.val()
      itemEve.id = snapshot.key
      ve.foodsEvening.push(itemEve)
    })
    foodsEvening.on('child_removed', function (snapshot) {
      var idEve = snapshot.key
      ve.foodsEvening.splice(ve.foodsEvening.findIndex(foodEve => foodEve.id === idEve), 1)
    })
    blueUsers.on('child_added', function (snapshot) {
      var itemBlueUsers = snapshot.val()
      itemBlueUsers.id = snapshot.key
      vm.blueUsers.push(itemBlueUsers)
    })
    blueUsers.on('child_removed', function (snapshot) {
      var idBlueUsers = snapshot.key
      vm.blueUsers.splice(vm.blueUsers.findIndex(blueUsers => blueUsers.id === idBlueUsers), 1)
    })
    blueUsers.on('child_changed', function (snapshot) {
      var idBlueUsers = snapshot.key
      var blueUsersFind = vm.blueUsers.find(blueUsers => blueUsers.id === idBlueUsers)
      blueUsersFind.temp = snapshot.val().temp
      blueUsersFind.foodMorningName = snapshot.val().foodMorningName
      blueUsersFind.foodAfternoonName = snapshot.val().foodAfternoonName
      blueUsersFind.foodEveningName = snapshot.val().foodEveningName
      if (vm.newBlueUsers === idBlueUsers) {
        vm.newBlueUsers.temp = snapshot.val().temp
        vm.newBlueUsers.foodMorningName = snapshot.val().foodMorningName
        vm.newBlueUsers.foodAfternoonName = snapshot.val().foodAfternoonName
        vm.newBlueUsers.foodEveningName = snapshot.val().foodEveningName
      }
    })
    greenUsers.on('child_added', function (snapshot) {
      var itemGreenUsers = snapshot.val()
      itemGreenUsers.id = snapshot.key
      vm.greenUsers.push(itemGreenUsers)
    })
    greenUsers.on('child_removed', function (snapshot) {
      var idGreenUsers = snapshot.key
      vm.greenUsers.splice(vm.greenUsers.findIndex(greenUsers => greenUsers.id === idGreenUsers), 1)
    })
    greenUsers.on('child_changed', function (snapshot) {
      var idGreenUsers = snapshot.key
      var greenUsersFind = vm.greenUsers.find(greenUsers => greenUsers.id === idGreenUsers)
      greenUsersFind.temp = snapshot.val().temp
      greenUsersFind.foodMorningName = snapshot.val().foodMorningName
      greenUsersFind.foodAfternoonName = snapshot.val().foodAfternoonName
      greenUsersFind.foodEveningName = snapshot.val().foodEveningName
      if (vm.newGreenUsers === idGreenUsers) {
        vm.newGreenUsers.temp = snapshot.val().temp
        vm.newGreenUsers.foodMorningName = snapshot.val().foodMorningName
        vm.newGreenUsers.foodAfternoonName = snapshot.val().foodAfternoonName
        vm.newGreenUsers.foodEveningName = snapshot.val().foodEveningName
      }
    })
    orangeUsers.on('child_added', function (snapshot) {
      var itemOrangeUsers = snapshot.val()
      itemOrangeUsers.id = snapshot.key
      vm.orangeUsers.push(itemOrangeUsers)
    })
    orangeUsers.on('child_removed', function (snapshot) {
      var idOrangeUsers = snapshot.key
      vm.orangeUsers.splice(vm.orangeUsers.findIndex(orangeUsers => orangeUsers.id === idOrangeUsers), 1)
    })
    orangeUsers.on('child_changed', function (snapshot) {
      var idOrangeUsers = snapshot.key
      var orangeUsersFind = vm.orangeUsers.find(orangeUsers => orangeUsers.id === idOrangeUsers)
      orangeUsersFind.temp = snapshot.val().temp
      orangeUsersFind.foodMorningName = snapshot.val().foodMorningName
      orangeUsersFind.foodAfternoonName = snapshot.val().foodAfternoonName
      orangeUsersFind.foodEveningName = snapshot.val().foodEveningName
      if (vm.newOrangeUsers === idOrangeUsers) {
        vm.newOrangeUsers.temp = snapshot.val().temp
        vm.newOrangeUsers.foodMorningName = snapshot.val().foodMorningName
        vm.newOrangeUsers.foodAfternoonName = snapshot.val().foodAfternoonName
        vm.newOrangeUsers.foodEveningName = snapshot.val().foodEveningName
      }
    })
    pinkUsers.on('child_added', function (snapshot) {
      var itemPinkUsers = snapshot.val()
      itemPinkUsers.id = snapshot.key
      vm.pinkUsers.push(itemPinkUsers)
    })
    pinkUsers.on('child_removed', function (snapshot) {
      var idPinkUsers = snapshot.key
      vm.pinkUsers.splice(vm.pinkUsers.findIndex(pinkUsers => pinkUsers.id === idPinkUsers), 1)
    })
    pinkUsers.on('child_changed', function (snapshot) {
      var idPinkUsers = snapshot.key
      var pinkUsersFind = vm.pinkUsers.find(pinkUsers => pinkUsers.id === idPinkUsers)
      pinkUsersFind.temp = snapshot.val().temp
      pinkUsersFind.foodMorningName = snapshot.val().foodMorningName
      pinkUsersFind.foodAfternoonName = snapshot.val().foodAfternoonName
      pinkUsersFind.foodEveningName = snapshot.val().foodEveningName
      if (vm.newPinkUsers === idPinkUsers) {
        vm.newPinkUsers.temp = snapshot.val().temp
        vm.newPinkUsers.foodMorningName = snapshot.val().foodMorningName
        vm.newPinkUsers.foodAfternoonName = snapshot.val().foodAfternoonName
        vm.newPinkUsers.foodEveningName = snapshot.val().foodEveningName
      }
    })
    checkOrder.on('child_added', function (snapshot) {
      var itemCheckOrder = snapshot.val()
      itemCheckOrder.id = snapshot.key
      vm.checkOrder.push(itemCheckOrder)
    })
    checkOrder.on('child_removed', function (snapshot) {
      var idCheckOrder = snapshot.key
      vm.checkOrder.splice(vm.checkOrder.findIndex(checkOrder => checkOrder.id === idCheckOrder), 1)
    })
    checkOrder.on('child_changed', function (snapshot) {
      var idCheckOrder = snapshot.key
      var checkOrderFind = vm.checkOrder.find(checkOrder => checkOrder.id === idCheckOrder)
      checkOrderFind.order = snapshot.val().order
      if (vm.newCheckOrder === idCheckOrder) {
        vm.newCheckOrder.order = snapshot.val().order
      }
    })
  },
  name: 'app',
  data () {
    return {
      buttonAdd: true,
      showOpen: true,
      buttonRemoveMor: true,
      buttonRemoveAfter: true,
      buttonRemoveEve: true,
      buttonEditMor: true,
      buttonEditAfter: true,
      buttonEditEve: true,
      deleteFoodMor: true,
      submitEditFoodMor: true,
      editMorBlueTwo: true,
      editAfterBlueTwo: true,
      editEveBlueTwo: true,
      editMorGreenTwo: true,
      editAfterGreenTwo: true,
      editEveGreenTwo: true,
      editMorOrangeTwo: true,
      editAfterOrangeTwo: true,
      editEveOrangeTwo: true,
      editMorPinkTwo: true,
      editAfterPinkTwo: true,
      editEvePinkTwo: true,
      ei: true,
      ei2: false,
      showEditButton: false,
      showEditButton2: false,
      showEditButton3: false,
      showEditButton4: false,
      checkShowMenuGreen: false,
      clickNameGreen: true,
      checkShowMenuBlue: false,
      clickNameBlue: true,
      checkShowMenuOrange: false,
      clickNameOrange: true,
      checkShowMenuPink: false,
      clickNamePink: true,
      back: true,
      show: true,
      blueHomeRemoveCheck: false,
      greenHomeRemoveCheck: false,
      orangeHomeRemoveCheck: false,
      pinkHomeRemoveCheck: false,
      showRemoveBlue: true,
      showRemoveGreen: true,
      showRemoveOrange: true,
      showRemovePink: true,
      showPlusBlue: true,
      showPlusGreen: true,
      showPlusOrange: true,
      showPlusPink: true,
      countFoodCheck: true,
      adminCheck: true,
      firstPage: true,
      guestPage: true,
      adminPage: true,
      checkAdmin: true,
      newAdmin: '',
      admin: '',
      newIdUser: '',
      newIdUserCheck: '',
      homes: '',
      check: false,
      statusManage: true,
      statusUsers: true,
      blueHomeCheck: false,
      checkInBlue: false,
      greenHomeCheck: false,
      checkInGreen: false,
      orangeHomeCheck: false,
      checkInOrange: false,
      pinkHomeCheck: false,
      checkInPink: false,
      home: false,
      foodsMorning: [],
      newFoodMorning: {
        foodName: ''
      },
      foodsAfternoon: [],
      newFoodAfternoon: {
        foodName: ''
      },
      foodsEvening: [],
      newFoodEvening: {
        foodName: ''
      },
      checkOrder: [],
      newCheckOrder: {
        order: true
      },
      blueUsers: [],
      newBlueUsers: {
        idUser: '',
        idCard: '',
        inputPass: '',
        temp: false,
        home: 'บ้านฟ้า',
        name: '',
        foodMorningName: '',
        foodAfternoonName: '',
        foodEveningName: ''
      },
      greenUsers: [],
      newGreenUsers: {
        idUser: '',
        idCard: '',
        inputPass: '',
        temp: false,
        home: 'บ้านเขียว',
        name: '',
        foodMorningName: '',
        foodAfternoonName: '',
        foodEveningName: ''
      },
      orangeUsers: [],
      newOrangeUsers: {
        idUser: '',
        idCard: '',
        inputPass: '',
        temp: false,
        home: 'บ้านส้ม',
        name: '',
        foodMorningName: '',
        foodAfternoonName: '',
        foodEveningName: ''
      },
      pinkUsers: [],
      newPinkUsers: {
        idUser: '',
        idCard: '',
        inputPass: '',
        temp: false,
        home: 'บ้านชมพู',
        name: '',
        foodMorningName: '',
        foodAfternoonName: '',
        foodEveningName: ''
      }
    }
  },
  methods: {
    timeUp (id) {
      var vm = this
      firebase.database().ref('checkOrder/' + id).update({
        order: vm.newCheckOrder.order = false
      })
      swal('ตัดยอดสั่งข้าวสำเร็จ', 'กดปุ่ม OK', 'success')
    },
    openOder (id) {
      var vm = this
      firebase.database().ref('checkOrder/' + id).update({
        order: vm.newCheckOrder.order = true
      })
      swal('เปิดสั่งข้าวสำเร็จ', 'กดปุ่ม OK', 'success')
    },
    addCheckOrder: function () {
      let result = checkOrder.push(this.newCheckOrder)
      this.newCheckOrder.id = result.key
    },
    cancleClickNameBlue (id) {
      var vm = this
      firebase.database().ref('blueUsers/' + id).update({
        temp: vm.newBlueUsers.temp = false
      })
      this.clickNameBlue = true
      this.ei = true
      this.ei2 = false
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.idCard = ''
    },
    cancleClickNameGreen (id) {
      var vm = this
      firebase.database().ref('greenUsers/' + id).update({
        temp: vm.newGreenUsers.temp = false
      })
      this.clickNameGreen = true
      this.ei = true
      this.ei2 = false
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.idCard = ''
    },
    cancleClickNameOrange (id) {
      var vm = this
      firebase.database().ref('orangeUsers/' + id).update({
        temp: vm.newOrangeUsers.temp = false
      })
      this.clickNameOrange = true
      this.ei = true
      this.ei2 = false
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.idCard = ''
    },
    cancleClickNamePink (id) {
      var vm = this
      firebase.database().ref('pinkUsers/' + id).update({
        temp: vm.newPinkUsers.temp = false
      })
      this.clickNamePink = true
      this.ei = true
      this.ei2 = false
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.idCard = ''
    },
    addFoodSuccess (idCard) {
      if (idCard !== this.newBlueUsers.idCard && idCard !== this.newGreenUsers.idCard && idCard !== this.newOrangeUsers.idCard && idCard !== this.newPinkUsers.idCard) {
        this.newBlueUsers.idCard = ''
        this.newGreenUsers.idCard = ''
        this.newOrangeUsers.idCard = ''
        this.newPinkUsers.idCard = ''
      }
      if (idCard === this.newBlueUsers.idCard) {
        this.checkShowMenuBlue = true
        this.showEditButton3 = false
        this.submitEditFoodMor = true
        this.newBlueUsers.idCard = ''
        this.buttonAdd = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.showEditButton = true
        this.showEditButton2 = false
      }
      if (idCard === this.newGreenUsers.idCard) {
        this.checkShowMenuGreen = true
        this.showEditButton3 = false
        this.submitEditFoodMor = true
        this.newGreenUsers.idCard = ''
        this.buttonAdd = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.showEditButton = true
        this.showEditButton2 = false
      }
      if (idCard === this.newOrangeUsers.idCard) {
        this.checkShowMenuOrange = true
        this.showEditButton3 = false
        this.submitEditFoodMor = true
        this.newOrangeUsers.idCard = ''
        this.buttonAdd = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.showEditButton = true
        this.showEditButton2 = false
      }
      if (idCard === this.newPinkUsers.idCard) {
        this.checkShowMenuPink = true
        this.showEditButton3 = false
        this.submitEditFoodMor = true
        this.newPinkUsers.idCard = ''
        this.buttonAdd = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.showEditButton = true
        this.showEditButton2 = false
      }
    },
    openFoodsBlueUser (id) {
      this.showOpen = false
      this.submitEditFoodMor = false
      this.showEditButton3 = true
      this.buttonAdd = false
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.buttonEditMor = true
      this.buttonEditAfter = true
      this.buttonEditEve = true
      this.showEditButton = true
      this.showEditButton2 = false
    },
    openFoodsGreenUser (id) {
      this.showOpen = false
      this.submitEditFoodMor = false
      this.showEditButton3 = true
      this.buttonAdd = false
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.buttonEditMor = true
      this.buttonEditAfter = true
      this.buttonEditEve = true
      this.showEditButton = true
      this.showEditButton2 = false
    },
    openFoodsOrangeUser (id) {
      this.showOpen = false
      this.submitEditFoodMor = false
      this.showEditButton3 = true
      this.buttonAdd = false
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.buttonEditMor = true
      this.buttonEditAfter = true
      this.buttonEditEve = true
      this.showEditButton = true
      this.showEditButton2 = false
    },
    openFoodsPinkUser (id) {
      this.showOpen = false
      this.submitEditFoodMor = false
      this.showEditButton3 = true
      this.buttonAdd = false
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.buttonEditMor = true
      this.buttonEditAfter = true
      this.buttonEditEve = true
      this.showEditButton = true
      this.showEditButton2 = false
    },
    cancleEditPass () {
      this.submitEditFoodMor = true
      this.submitEditFoodAfter = true
      this.submitEditFoodEve = true
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.deleteFoodMor = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.idCard = ''
    },
    removeEditPass () {
      this.submitEditFoodMor = true
      this.submitEditFoodAfter = true
      this.submitEditFoodEve = true
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.deleteFoodMor = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
      this.showOpen = true
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.idCard = ''
    },
    deleteFoodBlueMorSuccess (id, idCard) {
      if (idCard === this.newBlueUsers.idCard) {
        this.deleteFoodMor = true
        var vm = this
        firebase.database().ref('blueUsers/' + id).update({
          foodMorningName: vm.newBlueUsers.foodMorningName = '',
          foodAfternoonName: vm.newBlueUsers.foodAfternoonName = '',
          foodEveningName: vm.newBlueUsers.foodEveningName = '',
          temp: vm.newBlueUsers.temp = true
        })
        this.newBlueUsers.idCard = ''
        this.checkShowMenuBlue = false
        this.ei = true
        this.ei2 = false
      } else {
        this.newBlueUsers.idCard = ''
      }
    },
    deleteFoodGreenMorSuccess (id, idCard) {
      if (idCard === this.newGreenUsers.idCard) {
        this.deleteFoodMor = true
        var vm = this
        firebase.database().ref('greenUsers/' + id).update({
          foodMorningName: vm.newGreenUsers.foodMorningName = '',
          foodAfternoonName: vm.newGreenUsers.foodAfternoonName = '',
          foodEveningName: vm.newGreenUsers.foodEveningName = '',
          temp: vm.newGreenUsers.temp = true
        })
        this.newGreenUsers.idCard = ''
        this.checkShowMenuGreen = false
        this.ei = true
        this.ei2 = false
      } else {
        this.newGreenUsers.idCard = ''
      }
    },
    deleteFoodOrangeMorSuccess (id, idCard) {
      if (idCard === this.newOrangeUsers.idCard) {
        this.deleteFoodMor = true
        var vm = this
        firebase.database().ref('orangeUsers/' + id).update({
          foodMorningName: vm.newOrangeUsers.foodMorningName = '',
          foodAfternoonName: vm.newOrangeUsers.foodAfternoonName = '',
          foodEveningName: vm.newOrangeUsers.foodEveningName = '',
          temp: vm.newOrangeUsers.temp = true
        })
        this.newOrangeUsers.idCard = ''
        this.checkShowMenuOrange = false
        this.ei = true
        this.ei2 = false
      } else {
        this.newOrangeUsers.idCard = ''
      }
    },
    deleteFoodPinkMorSuccess (id, idCard) {
      if (idCard === this.newPinkUsers.idCard) {
        this.deleteFoodMor = true
        var vm = this
        firebase.database().ref('pinkUsers/' + id).update({
          foodMorningName: vm.newPinkUsers.foodMorningName = '',
          foodAfternoonName: vm.newPinkUsers.foodAfternoonName = '',
          foodEveningName: vm.newPinkUsers.foodEveningName = '',
          temp: vm.newPinkUsers.temp = true
        })
        this.newPinkUsers.idCard = ''
        this.checkShowMenuPink = false
        this.ei = true
        this.ei2 = false
      } else {
        this.newPinkUsers.idCard = ''
      }
    },
    removeFoodsBlueUser () {
      this.deleteFoodMor = false
      this.submitEditFoodMor = true
      this.showEditButton4 = true
      this.showOpen = false
    },
    removeFoodsGreenUser () {
      this.deleteFoodMor = false
      this.submitEditFoodMor = true
      this.showEditButton4 = true
      this.showOpen = false
    },
    removeFoodsOrangeUser () {
      this.deleteFoodMor = false
      this.submitEditFoodMor = true
      this.showEditButton4 = true
      this.showOpen = false
    },
    removeFoodsPinkUser () {
      this.deleteFoodMor = false
      this.submitEditFoodMor = true
      this.showEditButton4 = true
      this.showOpen = false
    },
    removeFoodMorSuccess (id, idCard) {
      if (idCard !== this.newBlueUsers.idCard && idCard !== this.newGreenUsers.idCard && idCard !== this.newOrangeUsers.idCard && idCard !== this.newPinkUsers.idCard) {
        this.newBlueUsers.idCard = ''
        this.newGreenUsers.idCard = ''
        this.newOrangeUsers.idCard = ''
        this.newPinkUsers.idCard = ''
      }
      var vm = this
      if (idCard === this.newBlueUsers.idCard) {
        firebase.database().ref('blueUsers/' + id).update({
          foodMorningName: vm.newBlueUsers.foodMorningName = ''
        })
        this.checkShowMenuBlue = false
        this.submitEditFoodMor = true
        this.showOpen = true
        this.newBlueUsers.idCard = ''
        this.ei = true
        this.ei2 = false
      }
      if (idCard === this.newGreenUsers.idCard) {
        firebase.database().ref('greenUsers/' + id).update({
          foodMorningName: vm.newGreenUsers.foodMorningName = ''
        })
        this.checkShowMenuGreen = false
        this.submitEditFoodMor = true
        this.showOpen = true
        this.newGreenUsers.idCard = ''
        this.ei = true
        this.ei2 = false
      }
      if (idCard === this.newOrangeUsers.idCard) {
        firebase.database().ref('orangeUsers/' + id).update({
          foodMorningName: vm.newOrangeUsers.foodMorningName = ''
        })
        this.checkShowMenuOrange = false
        this.submitEditFoodMor = true
        this.showOpen = true
        this.newOrangeUsers.idCard = ''
        this.ei = true
        this.ei2 = false
      }
      if (idCard === this.newPinkUsers.idCard) {
        firebase.database().ref('pinkUsers/' + id).update({
          foodMorningName: vm.newPinkUsers.foodMorningName = ''
        })
        this.checkShowMenuPink = false
        this.submitEditFoodMor = true
        this.showOpen = true
        this.newPinkUsers.idCard = ''
        this.ei = true
        this.ei2 = false
      }
    },
    removeFoodAfterSuccess (id, idCard) {
      if (idCard !== this.newBlueUsers.idCard && idCard !== this.newGreenUsers.idCard && idCard !== this.newOrangeUsers.idCard && idCard !== this.newPinkUsers.idCard) {
        this.newBlueUsers.idCard = ''
        this.newGreenUsers.idCard = ''
        this.newOrangeUsers.idCard = ''
        this.newPinkUsers.idCard = ''
      }
      var vm = this
      if (idCard === this.newBlueUsers.idCard) {
        firebase.database().ref('blueUsers/' + id).update({
          foodAfternoonName: vm.newBlueUsers.foodAfternoonName = ''
        })
        this.checkShowMenuBlue = false
        this.submitEditFoodMor = true
        this.showOpen = true
        this.newBlueUsers.idCard = ''
        this.ei = true
        this.ei2 = false
      }
      if (idCard === this.newGreenUsers.idCard) {
        firebase.database().ref('greenUsers/' + id).update({
          foodAfternoonName: vm.newGreenUsers.foodAfternoonName = ''
        })
        this.checkShowMenuGreen = false
        this.submitEditFoodMor = true
        this.showOpen = true
        this.newGreenUsers.idCard = ''
        this.ei = true
        this.ei2 = false
      }
      if (idCard === this.newOrangeUsers.idCard) {
        firebase.database().ref('orangeUsers/' + id).update({
          foodAfternoonName: vm.newOrangeUsers.foodAfternoonName = ''
        })
        this.checkShowMenuOrange = false
        this.submitEditFoodMor = true
        this.showOpen = true
        this.newOrangeUsers.idCard = ''
        this.ei = true
        this.ei2 = false
      }
      if (idCard === this.newPinkUsers.idCard) {
        firebase.database().ref('pinkUsers/' + id).update({
          foodAfternoonName: vm.newPinkUsers.foodAfternoonName = ''
        })
        this.checkShowMenuPink = false
        this.submitEditFoodMor = true
        this.showOpen = true
        this.newPinkUsers.idCard = ''
        this.ei = true
        this.ei2 = false
      }
    },
    removeFoodEveSuccess (id, idCard) {
      if (idCard !== this.newBlueUsers.idCard && idCard !== this.newGreenUsers.idCard && idCard !== this.newOrangeUsers.idCard && idCard !== this.newPinkUsers.idCard) {
        this.newBlueUsers.idCard = ''
        this.newGreenUsers.idCard = ''
        this.newOrangeUsers.idCard = ''
        this.newPinkUsers.idCard = ''
      }
      var vm = this
      if (idCard === this.newBlueUsers.idCard) {
        firebase.database().ref('blueUsers/' + id).update({
          foodEveningName: vm.newBlueUsers.foodEveningName = ''
        })
        this.checkShowMenuBlue = false
        this.submitEditFoodMor = true
        this.showOpen = true
        this.newBlueUsers.idCard = ''
        this.ei = true
        this.ei2 = false
      }
      if (idCard === this.newGreenUsers.idCard) {
        firebase.database().ref('greenUsers/' + id).update({
          foodEveningName: vm.newGreenUsers.foodEveningName = ''
        })
        this.checkShowMenuGreen = false
        this.submitEditFoodMor = true
        this.showOpen = true
        this.newGreenUsers.idCard = ''
        this.ei = true
        this.ei2 = false
      }
      if (idCard === this.newOrangeUsers.idCard) {
        firebase.database().ref('orangeUsers/' + id).update({
          foodEveningName: vm.newOrangeUsers.foodEveningName = ''
        })
        this.checkShowMenuOrange = false
        this.submitEditFoodMor = true
        this.showOpen = true
        this.newOrangeUsers.idCard = ''
        this.ei = true
        this.ei2 = false
      }
      if (idCard === this.newPinkUsers.idCard) {
        firebase.database().ref('pinkUsers/' + id).update({
          foodEveningName: vm.newPinkUsers.foodEveningName = ''
        })
        this.checkShowMenuPink = false
        this.submitEditFoodMor = true
        this.showOpen = true
        this.newPinkUsers.idCard = ''
        this.ei = true
        this.ei2 = false
      }
    },
    editFoodMorSuccess (id, idCard) {
      if (idCard !== this.newBlueUsers.idCard && idCard !== this.newGreenUsers.idCard && idCard !== this.newOrangeUsers.idCard && idCard !== this.newPinkUsers.idCard) {
        this.newBlueUsers.idCard = ''
        this.newGreenUsers.idCard = ''
        this.newOrangeUsers.idCard = ''
        this.newPinkUsers.idCard = ''
      }
      if (idCard === this.newBlueUsers.idCard) {
        this.editMorBlueTwo = false
        this.editAfterBlueTwo = true
        this.editEveBlueTwo = true
        this.submitEditFoodMor = true
        this.newBlueUsers.idCard = ''
        this.showEditButton = true
        this.showEditButton2 = false
        this.buttonAdd = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
      }
      if (idCard === this.newGreenUsers.idCard) {
        this.editMorGreenTwo = false
        this.editAfterGreenTwo = true
        this.editEveGreenTwo = true
        this.submitEditFoodMor = true
        this.newGreenUsers.idCard = ''
        this.showEditButton = true
        this.showEditButton2 = false
        this.buttonAdd = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
      }
      if (idCard === this.newOrangeUsers.idCard) {
        this.editMorOrangeTwo = false
        this.editAfterOrangeTwo = true
        this.editEveOrangeTwo = true
        this.submitEditFoodMor = true
        this.newOrangeUsers.idCard = ''
        this.showEditButton = true
        this.showEditButton2 = false
        this.buttonAdd = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
      }
      if (idCard === this.newPinkUsers.idCard) {
        this.editMorPinkTwo = false
        this.editAfterPinkTwo = true
        this.editEvePinkTwo = true
        this.submitEditFoodMor = true
        this.newPinkUsers.idCard = ''
        this.showEditButton = true
        this.showEditButton2 = false
        this.buttonAdd = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
      }
    },
    editFoodAfterSuccess (id, idCard) {
      if (idCard !== this.newBlueUsers.idCard && idCard !== this.newGreenUsers.idCard && idCard !== this.newOrangeUsers.idCard && idCard !== this.newPinkUsers.idCard) {
        this.newBlueUsers.idCard = ''
        this.newGreenUsers.idCard = ''
        this.newOrangeUsers.idCard = ''
        this.newPinkUsers.idCard = ''
      }
      if (idCard === this.newBlueUsers.idCard) {
        this.editMorBlueTwo = true
        this.editAfterBlueTwo = false
        this.editEveBlueTwo = true
        this.submitEditFoodMor = true
        this.newBlueUsers.idCard = ''
        this.showEditButton = true
        this.showEditButton2 = false
        this.buttonAdd = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
      }
      if (idCard === this.newGreenUsers.idCard) {
        this.editMorGreenTwo = true
        this.editAfterGreenTwo = false
        this.editEveGreenTwo = true
        this.submitEditFoodMor = true
        this.newGreenUsers.idCard = ''
        this.showEditButton = true
        this.showEditButton2 = false
        this.buttonAdd = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
      }
      if (idCard === this.newOrangeUsers.idCard) {
        this.editMorOrangeTwo = true
        this.editAfterOrangeTwo = false
        this.editEveOrangeTwo = true
        this.submitEditFoodMor = true
        this.newOrangeUsers.idCard = ''
        this.showEditButton = true
        this.showEditButton2 = false
        this.buttonAdd = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
      }
      if (idCard === this.newPinkUsers.idCard) {
        this.editMorPinkTwo = true
        this.editAfterPinkTwo = false
        this.editEvePinkTwo = true
        this.submitEditFoodMor = true
        this.newPinkUsers.idCard = ''
        this.showEditButton = true
        this.showEditButton2 = false
        this.buttonAdd = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
      }
    },
    editFoodEveSuccess (id, idCard) {
      if (idCard !== this.newBlueUsers.idCard && idCard !== this.newGreenUsers.idCard && idCard !== this.newOrangeUsers.idCard && idCard !== this.newPinkUsers.idCard) {
        this.newBlueUsers.idCard = ''
        this.newGreenUsers.idCard = ''
        this.newOrangeUsers.idCard = ''
        this.newPinkUsers.idCard = ''
      }
      if (idCard === this.newBlueUsers.idCard) {
        this.editMorBlueTwo = true
        this.editAfterBlueTwo = true
        this.editEveBlueTwo = false
        this.submitEditFoodMor = true
        this.newBlueUsers.idCard = ''
        this.showEditButton = true
        this.showEditButton2 = false
        this.buttonAdd = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
      }
      if (idCard === this.newGreenUsers.idCard) {
        this.editMorGreenTwo = true
        this.editAfterGreenTwo = true
        this.editEveGreenTwo = false
        this.submitEditFoodMor = true
        this.newGreenUsers.idCard = ''
        this.showEditButton = true
        this.showEditButton2 = false
        this.buttonAdd = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
      }
      if (idCard === this.newOrangeUsers.idCard) {
        this.editMorOrangeTwo = true
        this.editAfterOrangeTwo = true
        this.editEveOrangeTwo = false
        this.submitEditFoodMor = true
        this.newOrangeUsers.idCard = ''
        this.showEditButton = true
        this.showEditButton2 = false
        this.buttonAdd = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
      }
      if (idCard === this.newPinkUsers.idCard) {
        this.editMorPinkTwo = true
        this.editAfterPinkTwo = true
        this.editEvePinkTwo = false
        this.submitEditFoodMor = true
        this.newPinkUsers.idCard = ''
        this.showEditButton = true
        this.showEditButton2 = false
        this.buttonAdd = true
        this.buttonEditMor = true
        this.buttonEditAfter = true
        this.buttonEditEve = true
        this.buttonRemoveMor = true
        this.buttonRemoveAfter = true
        this.buttonRemoveEve = true
      }
    },
    cancleEdit () {
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.editMorBlueTwo = true
      this.editAfterBlueTwo = true
      this.editEveBlueTwo = true
      this.editMorGreenTwo = true
      this.editAfterGreenTwo = true
      this.editEveGreenTwo = true
      this.editMorOrangeTwo = true
      this.editAfterOrangeTwo = true
      this.editEveOrangeTwo = true
      this.editMorPinkTwo = true
      this.editAfterPinkTwo = true
      this.editEvePinkTwo = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
    },
    cancleFoodMor () {
      this.showEditButton3 = true
      this.editMorBlueTwo = true
      this.editAfterBlueTwo = true
      this.editEveBlueTwo = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonRemoveMor = false
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.buttonEditMor = true
      this.buttonEditAfter = true
      this.buttonEditEve = true
      this.buttonAdd = true
      this.showEditButton = true
      this.showEditButton2 = false
    },
    cancleFoodAfter () {
      this.showEditButton3 = true
      this.editMorBlueTwo = true
      this.editAfterBlueTwo = true
      this.editEveBlueTwo = true
      this.submitEditFoodMor = false
      this.buttonRemoveMor = true
      this.deleteFoodMor = true
      this.buttonRemoveAfter = false
      this.buttonRemoveEve = true
      this.buttonEditMor = true
      this.buttonEditAfter = true
      this.buttonEditEve = true
      this.buttonAdd = true
      this.showEditButton = true
      this.showEditButton2 = false
    },
    cancleFoodEve () {
      this.showEditButton3 = true
      this.editMorBlueTwo = true
      this.editAfterBlueTwo = true
      this.editEveBlueTwo = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonRemoveEve = false
      this.buttonRemoveAfter = true
      this.buttonRemoveMor = true
      this.buttonEditMor = true
      this.buttonEditAfter = true
      this.buttonEditEve = true
      this.buttonAdd = true
      this.showEditButton = true
      this.showEditButton2 = false
    },
    editMorBlue () {
      this.showEditButton3 = true
      this.editMorBlueTwo = true
      this.editAfterBlueTwo = true
      this.editEveBlueTwo = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonEditMor = false
      this.buttonEditAfter = true
      this.buttonEditEve = true
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
    },
    editMorGreen () {
      this.showEditButton3 = true
      this.editMorGreenTwo = true
      this.editAfterGreenTwo = true
      this.editEveGreenTwo = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonEditMor = false
      this.buttonEditAfter = true
      this.buttonEditEve = true
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
    },
    editMorOrange () {
      this.showEditButton3 = true
      this.editMorOrangeTwo = true
      this.editAfterOrangeTwo = true
      this.editEveOrangeTwo = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonEditMor = false
      this.buttonEditAfter = true
      this.buttonEditEve = true
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
    },
    editMorPink () {
      this.showEditButton3 = true
      this.editMorPinkTwo = true
      this.editAfterPinkTwo = true
      this.editEvePinkTwo = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonEditMor = false
      this.buttonEditAfter = true
      this.buttonEditEve = true
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
    },
    editAfterBlue () {
      this.showEditButton3 = true
      this.editAfterBlueTwo = true
      this.editEveBlueTwo = true
      this.editMorBlueTwo = true
      this.deleteFoodMor = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonEditMor = true
      this.buttonEditAfter = false
      this.buttonEditEve = true
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
    },
    editAfterGreen () {
      this.showEditButton3 = true
      this.editAfterGreenTwo = true
      this.editEveGreenTwo = true
      this.editMorGreenTwo = true
      this.deleteFoodMor = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonEditMor = true
      this.buttonEditAfter = false
      this.buttonEditEve = true
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
    },
    editAfterOrange () {
      this.showEditButton3 = true
      this.editAfterOrangeTwo = true
      this.editEveOrangeTwo = true
      this.editMorOrangeTwo = true
      this.deleteFoodMor = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonEditMor = true
      this.buttonEditAfter = false
      this.buttonEditEve = true
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
    },
    editAfterPink () {
      this.showEditButton3 = true
      this.editAfterPinkTwo = true
      this.editEvePinkTwo = true
      this.editMorPinkTwo = true
      this.deleteFoodMor = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonEditMor = true
      this.buttonEditAfter = false
      this.buttonEditEve = true
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
    },
    editEveBlue () {
      this.showEditButton3 = true
      this.editEveBlueTwo = true
      this.editMorBlueTwo = true
      this.editAfterBlueTwo = true
      this.deleteFoodMor = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonEditMor = true
      this.buttonEditAfter = true
      this.buttonEditEve = false
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
    },
    editEveGreen () {
      this.showEditButton3 = true
      this.editEveGreenTwo = true
      this.editMorGreenTwo = true
      this.editAfterGreenTwo = true
      this.deleteFoodMor = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonEditMor = true
      this.buttonEditAfter = true
      this.buttonEditEve = false
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
    },
    editEveOrange () {
      this.showEditButton3 = true
      this.editEveOrangeTwo = true
      this.editMorOrangeTwo = true
      this.editAfterOrangeTwo = true
      this.deleteFoodMor = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonEditMor = true
      this.buttonEditAfter = true
      this.buttonEditEve = false
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
    },
    editEvePink () {
      this.showEditButton3 = true
      this.editEvePinkTwo = true
      this.editMorPinkTwo = true
      this.editAfterPinkTwo = true
      this.deleteFoodMor = true
      this.submitEditFoodMor = false
      this.deleteFoodMor = true
      this.buttonEditMor = true
      this.buttonEditAfter = true
      this.buttonEditEve = false
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.showEditButton = true
      this.showEditButton2 = false
      this.buttonAdd = true
    },
    checkClickGreen (idCard) {
      if (idCard === this.newGreenUsers.idCard) {
        this.checkShowMenuGreen = true
        this.newGreenUsers.idCard = ''
        this.clickNameGreen = true
        this.showOpen = false
      } else {
        this.newGreenUsers.idCard = ''
      }
    },
    checkClickBlue (idCard) {
      if (idCard === this.newBlueUsers.idCard) {
        this.checkShowMenuBlue = true
        this.newBlueUsers.idCard = ''
        this.clickNameBlue = true
        this.showOpen = false
      } else {
        this.newBlueUsers.idCard = ''
      }
    },
    checkClickOrange (idCard) {
      if (idCard === this.newOrangeUsers.idCard) {
        this.checkShowMenuOrange = true
        this.newOrangeUsers.idCard = ''
        this.clickNameOrange = true
        this.showOpen = false
      } else {
        this.newOrangeUsers.idCard = ''
      }
    },
    checkClickPink (idCard) {
      if (idCard === this.newPinkUsers.idCard) {
        this.checkShowMenuPink = true
        this.newPinkUsers.idCard = ''
        this.clickNamePink = true
        this.showOpen = false
      } else {
        this.newPinkUsers.idCard = ''
      }
    },
    blueHomeRemove () {
      this.blueHomeRemoveCheck = true
      this.showPlusGreen = false
      this.showPlusOrange = false
      this.showPlusPink = false
      this.showPlusBlue = false
      this.showRemoveBlue = false
      this.showRemoveGreen = false
      this.showRemoveOrange = false
      this.showRemovePink = false
      this.show = false
    },
    deleteBlueUser (usersBlue) {
      firebase.database().ref('blueUsers/' + usersBlue.id).remove()
    },
    greenHomeRemove () {
      this.greenHomeRemoveCheck = true
      this.showPlusGreen = false
      this.showPlusOrange = false
      this.showPlusPink = false
      this.showPlusBlue = false
      this.showRemoveBlue = false
      this.showRemoveGreen = false
      this.showRemoveOrange = false
      this.showRemovePink = false
      this.show = false
    },
    deleteGreenUser (usersGreen) {
      firebase.database().ref('greenUsers/' + usersGreen.id).remove()
    },
    orangeHomeRemove () {
      this.orangeHomeRemoveCheck = true
      this.showPlusGreen = false
      this.showPlusOrange = false
      this.showPlusPink = false
      this.showPlusBlue = false
      this.showRemoveBlue = false
      this.showRemoveGreen = false
      this.showRemoveOrange = false
      this.showRemovePink = false
      this.show = false
    },
    deleteOrangeUser (usersOrange) {
      firebase.database().ref('orangeUsers/' + usersOrange.id).remove()
    },
    pinkHomeRemove () {
      this.pinkHomeRemoveCheck = true
      this.showPlusGreen = false
      this.showPlusOrange = false
      this.showPlusPink = false
      this.showPlusBlue = false
      this.showRemoveBlue = false
      this.showRemoveGreen = false
      this.showRemoveOrange = false
      this.showRemovePink = false
      this.show = false
    },
    deletePinkUser (usersPink) {
      firebase.database().ref('pinkUsers/' + usersPink.id).remove()
    },
    removeFoodsBlue (id) {
      var vm = this
      firebase.database().ref('blueUsers/' + id).update({
        foodMorningName: vm.newBlueUsers.foodMorningName = '',
        foodAfternoonName: vm.newBlueUsers.foodAfternoonName = '',
        foodEveningName: vm.newBlueUsers.foodEveningName = '',
        temp: vm.newBlueUsers.temp = false
      })
    },
    removeFoodsGreen (id) {
      var vm = this
      firebase.database().ref('greenUsers/' + id).update({
        foodMorningName: vm.newGreenUsers.foodMorningName = '',
        foodAfternoonName: vm.newGreenUsers.foodAfternoonName = '',
        foodEveningName: vm.newGreenUsers.foodEveningName = '',
        temp: vm.newGreenUsers.temp = false
      })
    },
    removeFoodsOrange (id) {
      var vm = this
      firebase.database().ref('orangeUsers/' + id).update({
        foodMorningName: vm.newOrangeUsers.foodMorningName = '',
        foodAfternoonName: vm.newOrangeUsers.foodAfternoonName = '',
        foodEveningName: vm.newOrangeUsers.foodEveningName = '',
        temp: vm.newOrangeUsers.temp = false
      })
    },
    removeFoodsPink (id) {
      var vm = this
      firebase.database().ref('pinkUsers/' + id).update({
        foodMorningName: vm.newPinkUsers.foodMorningName = '',
        foodAfternoonName: vm.newPinkUsers.foodAfternoonName = '',
        foodEveningName: vm.newPinkUsers.foodEveningName = '',
        temp: vm.newPinkUsers.temp = false
      })
    },
    countFoods () {
      this.countFoodCheck = false
      this.statusUsers = true
      this.statusManage = true
      this.homes = ''
      this.blueHomeCheck = false
      this.checkInBlue = false
      this.greenHomeCheck = false
      this.checkInGreen = false
      this.orangeHomeCheck = false
      this.checkInOrange = false
      this.pinkHomeCheck = false
      this.checkInPink = false
      this.blueHomeRemoveCheck = false
      this.greenHomeRemoveCheck = false
      this.orangeHomeRemoveCheck = false
      this.pinkHomeRemoveCheck = false
      this.newBlueUsers.name = ''
      this.newBlueUsers.idUser = ''
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.name = ''
      this.newGreenUsers.idUser = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.name = ''
      this.newOrangeUsers.idUser = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.name = ''
      this.newPinkUsers.idUser = ''
      this.newPinkUsers.idCard = ''
    },
    backFirstPage () {
      this.guestPage = true
      this.guestPage = true
      this.adminPage = true
      this.newIdUserCheck = ''
      this.newAdmin = ''
      this.homes = ''
      this.statusManage = true
      this.statusUsers = true
      this.adminCheck = true
      this.countFoodCheck = true
      this.show = true
      this.admin = ''
      this.newBlueUsers.name = ''
      this.newBlueUsers.idUser = ''
      this.newGreenUsers.name = ''
      this.newGreenUsers.idUser = ''
      this.newOrangeUsers.name = ''
      this.newOrangeUsers.idUser = ''
      this.newPinkUsers.name = ''
      this.newPinkUsers.idUser = ''
      this.newFoodMorning = ''
      this.newFoodAfternoon = ''
      this.newFoodEvening = ''
      this.back = true
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.idCard = ''
      this.clickNameGreen = true
      this.clickNameBlue = true
      this.clickNameOrange = true
      this.clickNamePink = true
      this.ei = true
      this.ei2 = false
      this.submitEditFoodMor = true
      this.deleteFoodMor = true
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.buttonEditMor = true
      this.buttonEditAfter = true
      this.buttonEditEve = true
      this.blueHomeRemoveCheck = false
      this.greenHomeRemoveCheck = false
      this.orangeHomeRemoveCheck = false
      this.pinkHomeRemoveCheck = false
      this.editMorBlueTwo = true
      this.editAfterBlueTwo = true
      this.editEveBlueTwo = true
      this.editMorGreenTwo = true
      this.editAfterGreenTwo = true
      this.editEveGreenTwo = true
      this.editMorOrangeTwo = true
      this.editAfterOrangeTwo = true
      this.editEveOrangeTwo = true
      this.editMorPinkTwo = true
      this.editAfterPinkTwo = true
      this.editEvePinkTwo = true
    },
    guestLogin () {
      this.guestPage = false
      this.firstPage = false
    },
    adminLogin () {
      this.adminPage = false
      this.firstPage = false
    },
    search (newIdUser) {
      this.newIdUserCheck = newIdUser
      if (this.newIdUserCheck === 'itkmutnb') {
        this.adminCheck = false
        this.checkAdmin = false
        this.adminPage = false
        this.guestPage = false
      }
      if (this.newIdUserCheck !== '') {
        this.back = false
      }
      this.newIdUser = ''
      this.checkShowMenuOrange = false
      this.checkShowMenuBlue = false
      this.checkShowMenuGreen = false
      this.checkShowMenuPink = false
      this.ei = true
      this.ei2 = false
      this.showEditButton = true
      this.showEditButton2 = false
      this.submitEditFoodMor = true
      this.deleteFoodMor = true
      this.showOpen = true
      this.buttonRemoveMor = true
      this.buttonRemoveAfter = true
      this.buttonRemoveEve = true
      this.buttonEditMor = true
      this.buttonEditAfter = true
      this.buttonEditEve = true
      this.editMorBlueTwo = true
      this.editAfterBlueTwo = true
      this.editEveBlueTwo = true
      this.editMorGreenTwo = true
      this.editAfterGreenTwo = true
      this.editEveGreenTwo = true
      this.editMorOrangeTwo = true
      this.editAfterOrangeTwo = true
      this.editEveOrangeTwo = true
      this.editMorPinkTwo = true
      this.editAfterPinkTwo = true
      this.editEvePinkTwo = true
    },
    logAdmin (admin) {
      this.newAdmin = admin
      this.admin = ''
    },
    home () {
      this.homes = ''
      this.statusManage = true
      this.statusUsers = true
    },
    blueHomeBacks () {
      this.blueHomeCheck = false
      this.showPlusGreen = true
      this.showPlusOrange = true
      this.showPlusPink = true
      this.showPlusBlue = true
      this.showRemoveBlue = true
      this.showRemoveGreen = true
      this.showRemoveOrange = true
      this.showRemovePink = true
      this.newBlueUsers.name = ''
      this.newBlueUsers.idUser = ''
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.name = ''
      this.newGreenUsers.idUser = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.name = ''
      this.newOrangeUsers.idUser = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.name = ''
      this.newPinkUsers.idUser = ''
      this.newPinkUsers.idCard = ''
      this.show = true
    },
    blueHomeChecks () {
      this.blueHomeCheck = true
      this.checkInBlue = true
      this.greenHomeCheck = false
      this.checkInGreen = false
      this.orangeHomeCheck = false
      this.checkInOrange = false
      this.pinkHomeCheck = false
      this.checkInPink = false
      this.countFoodCheck = true
      this.showPlusGreen = false
      this.showPlusOrange = false
      this.showPlusPink = false
      this.showPlusBlue = false
      this.showRemoveBlue = false
      this.showRemoveGreen = false
      this.showRemoveOrange = false
      this.showRemovePink = false
      this.show = false
    },
    addBlueUsers: function () {
      let result = blueUsers.push(this.newBlueUsers)
      this.newBlueUsers.id = result.key
      this.newBlueUsers.inputPass = ''
      this.newBlueUsers.temp = false
      this.newBlueUsers.name = ''
      this.newBlueUsers.idUser = ''
      this.newBlueUsers.idCard = ''
      this.newBlueUsers.foodMorningName = ''
      this.newBlueUsers.foodAfternoonName = ''
      this.newBlueUsers.foodEveningName = ''
      this.checkInBlue = false
      this.blueHomeCheck = false
      this.showPlusGreen = true
      this.showPlusOrange = true
      this.showPlusPink = true
      this.showPlusBlue = true
      this.showRemoveBlue = true
      this.showRemoveGreen = true
      this.showRemoveOrange = true
      this.showRemovePink = true
      this.show = true
    },
    pinkHomeBacks () {
      this.pinkHomeCheck = false
      this.showPlusGreen = true
      this.showPlusOrange = true
      this.showPlusBlue = true
      this.showPlusPink = true
      this.showRemoveBlue = true
      this.showRemoveGreen = true
      this.showRemoveOrange = true
      this.showRemovePink = true
      this.newPinkUsers.name = ''
      this.newPinkUsers.idUser = ''
      this.newPinkUsers.idCard = ''
      this.show = true
    },
    pinkHomeChecks () {
      this.pinkHomeCheck = true
      this.checkInPink = true
      this.greenHomeCheck = false
      this.checkInGreen = false
      this.orangeHomeCheck = false
      this.checkInOrange = false
      this.blueHomeCheck = false
      this.checkInBlue = false
      this.countFoodCheck = true
      this.showPlusGreen = false
      this.showPlusOrange = false
      this.showPlusBlue = false
      this.showPlusPink = false
      this.showRemoveBlue = false
      this.showRemoveGreen = false
      this.showRemoveOrange = false
      this.showRemovePink = false
      this.show = false
    },
    addPinkUsers: function () {
      let result = pinkUsers.push(this.newPinkUsers)
      this.newPinkUsers.id = result.key
      this.newPinkUsers.inputPass = ''
      this.newPinkUsers.temp = false
      this.newPinkUsers.name = ''
      this.newPinkUsers.idUser = ''
      this.newPinkUsers.idCard = ''
      this.newPinkUsers.foodMorningName = ''
      this.newPinkUsers.foodAfternoonName = ''
      this.newPinkUsers.foodEveningName = ''
      this.checkInPink = false
      this.pinkHomeCheck = false
      this.showPlusGreen = true
      this.showPlusOrange = true
      this.showPlusBlue = true
      this.showPlusPink = true
      this.show = true
      this.showRemoveBlue = true
      this.showRemoveGreen = true
      this.showRemoveOrange = true
      this.showRemovePink = true
    },
    greenHomeBacks () {
      this.greenHomeCheck = false
      this.showPlusGreen = true
      this.showPlusOrange = true
      this.showPlusBlue = true
      this.showPlusPink = true
      this.showRemoveBlue = true
      this.showRemoveGreen = true
      this.showRemoveOrange = true
      this.showRemovePink = true
      this.newGreenUsers.name = ''
      this.newGreenUsers.idUser = ''
      this.newGreenUsers.idCard = ''
      this.show = true
    },
    greenHomeChecks () {
      this.greenHomeCheck = true
      this.checkInGreen = true
      this.blueHomeCheck = false
      this.checkInBlue = false
      this.orangeHomeCheck = false
      this.checkInOrange = false
      this.pinkHomeCheck = false
      this.checkInPink = false
      this.countFoodCheck = true
      this.showPlusGreen = false
      this.showPlusOrange = false
      this.showPlusBlue = false
      this.showPlusPink = false
      this.showRemoveBlue = false
      this.showRemoveGreen = false
      this.showRemoveOrange = false
      this.showRemovePink = false
      this.show = false
    },
    addGreenUsers: function () {
      let result = greenUsers.push(this.newGreenUsers)
      this.newGreenUsers.id = result.key
      this.newGreenUsers.inputPass = ''
      this.newGreenUsers.temp = false
      this.newGreenUsers.name = ''
      this.newGreenUsers.idUser = ''
      this.newGreenUsers.idCard = ''
      this.newGreenUsers.foodMorningName = ''
      this.newGreenUsers.foodAfternoonName = ''
      this.newGreenUsers.foodEveningName = ''
      this.checkInGreen = false
      this.greenHomeCheck = false
      this.showPlusGreen = true
      this.showPlusOrange = true
      this.showPlusBlue = true
      this.showPlusPink = true
      this.show = true
      this.showRemoveBlue = true
      this.showRemoveGreen = true
      this.showRemoveOrange = true
      this.showRemovePink = true
    },
    orangeHomeBacks () {
      this.orangeHomeCheck = false
      this.showPlusGreen = true
      this.showPlusOrange = true
      this.showPlusPink = true
      this.showPlusBlue = true
      this.showRemoveBlue = true
      this.showRemoveGreen = true
      this.showRemoveOrange = true
      this.showRemovePink = true
      this.newOrangeUsers.name = ''
      this.newOrangeUsers.idUser = ''
      this.newOrangeUsers.idCard = ''
      this.show = true
    },
    orangeHomeChecks () {
      this.orangeHomeCheck = true
      this.checkInOrange = true
      this.blueHomeCheck = false
      this.checkInBlue = false
      this.greenHomeCheck = false
      this.checkInGreen = false
      this.pinkHomeCheck = false
      this.checkInPink = false
      this.countFoodCheck = true
      this.showPlusGreen = false
      this.showPlusOrange = false
      this.showPlusBlue = false
      this.showPlusPink = false
      this.showRemoveBlue = false
      this.showRemoveGreen = false
      this.showRemoveOrange = false
      this.showRemovePink = false
      this.show = false
    },
    addOrangeUsers: function () {
      let result = orangeUsers.push(this.newOrangeUsers)
      this.newOrangeUsers.id = result.key
      this.newOrangeUsers.inputPass = ''
      this.newOrangeUsers.temp = false
      this.newOrangeUsers.name = ''
      this.newOrangeUsers.idUser = ''
      this.newOrangeUsers.idCard = ''
      this.newOrangeUsers.foodMorningName = ''
      this.newOrangeUsers.foodAfternoonName = ''
      this.newOrangeUsers.foodEveningName = ''
      this.checkInOrange = false
      this.orangeHomeCheck = false
      this.showPlusGreen = true
      this.showPlusOrange = true
      this.showPlusBlue = true
      this.showPlusPink = true
      this.show = true
      this.showRemoveBlue = true
      this.showRemoveGreen = true
      this.showRemoveOrange = true
      this.showRemovePink = true
    },
    selectNameBlue (id) {
      var vm = this
      firebase.database().ref('blueUsers/' + id).update({
        temp: vm.newBlueUsers.temp = true
      })
      this.clickNameBlue = false
      this.checkShowMenuBlue = false
      this.showEditButton = false
      this.showEditButton2 = false
      this.ei = false
      this.ei2 = true
    },
    selectNameGreen (id) {
      var vm = this
      firebase.database().ref('greenUsers/' + id).update({
        temp: vm.newGreenUsers.temp = true
      })
      this.clickNameGreen = false
      this.checkShowMenuGreen = false
      this.showEditButton = false
      this.showEditButton2 = false
      this.ei = false
      this.ei2 = true
    },
    selectNameOrange (id) {
      var vm = this
      firebase.database().ref('orangeUsers/' + id).update({
        temp: vm.newOrangeUsers.temp = true
      })
      this.clickNameOrange = false
      this.checkShowMenuOrange = false
      this.showEditButton = false
      this.showEditButton2 = false
      this.ei = false
      this.ei2 = true
    },
    selectNamePink (id) {
      var vm = this
      firebase.database().ref('pinkUsers/' + id).update({
        temp: vm.newPinkUsers.temp = true
      })
      this.clickNamePink = false
      this.checkShowMenuPink = false
      this.showEditButton = false
      this.showEditButton2 = false
      this.ei = false
      this.ei2 = true
    },
    backBlue (id) {
      var vm = this
      firebase.database().ref('blueUsers/' + id).update({
        temp: vm.newBlueUsers.temp = false
      })
      this.checkShowMenuBlue = false
      this.ei = true
      this.ei2 = false
      this.showOpen = true
    },
    backPink (id) {
      var vm = this
      firebase.database().ref('pinkUsers/' + id).update({
        temp: vm.newPinkUsers.temp = false
      })
      this.checkShowMenuPink = false
      this.ei = true
      this.ei2 = false
      this.showOpen = true
    },
    backGreen (id) {
      var vm = this
      firebase.database().ref('greenUsers/' + id).update({
        temp: vm.newGreenUsers.temp = false
      })
      this.checkShowMenuGreen = false
      this.ei = true
      this.ei2 = false
      this.showOpen = true
    },
    backOrange (id) {
      var vm = this
      firebase.database().ref('orangeUsers/' + id).update({
        temp: vm.newOrangeUsers.temp = false
      })
      this.checkShowMenuOrange = false
      this.ei = true
      this.ei2 = false
      this.showOpen = true
    },
    addUsers: function () {
      this.statusUsers = false
      this.statusManage = true
      this.homes = ''
      this.blueHomeCheck = false
      this.checkInBlue = false
      this.greenHomeCheck = false
      this.checkInGreen = false
      this.orangeHomeCheck = false
      this.checkInOrange = false
      this.pinkHomeCheck = false
      this.checkInPink = false
      this.countFoodCheck = true
      this.showPlusPink = true
      this.showPlusBlue = true
      this.showPlusGreen = true
      this.showPlusOrange = true
      this.showRemoveBlue = true
      this.showRemoveGreen = true
      this.showRemoveOrange = true
      this.showRemovePink = true
      this.blueHomeRemoveCheck = false
      this.greenHomeRemoveCheck = false
      this.orangeHomeRemoveCheck = false
      this.pinkHomeRemoveCheck = false
      this.show = true
      this.newBlueUsers.name = ''
      this.newBlueUsers.idUser = ''
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.name = ''
      this.newGreenUsers.idUser = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.name = ''
      this.newOrangeUsers.idUser = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.name = ''
      this.newPinkUsers.idUser = ''
      this.newPinkUsers.idCard = ''
    },
    managerFoods: function () {
      this.statusManage = false
      this.homes = ''
      this.statusUsers = true
      this.blueHomeCheck = false
      this.checkInBlue = false
      this.greenHomeCheck = false
      this.checkInGreen = false
      this.orangeHomeCheck = false
      this.checkInOrange = false
      this.pinkHomeCheck = false
      this.checkInPink = false
      this.countFoodCheck = true
      this.blueHomeRemoveCheck = false
      this.greenHomeRemoveCheck = false
      this.orangeHomeRemoveCheck = false
      this.pinkHomeRemoveCheck = false
      this.show = true
      this.newBlueUsers.name = ''
      this.newBlueUsers.idUser = ''
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.name = ''
      this.newGreenUsers.idUser = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.name = ''
      this.newOrangeUsers.idUser = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.name = ''
      this.newPinkUsers.idUser = ''
      this.newPinkUsers.idCard = ''
    },
    addFoodsMorning: function () {
      foodsMorning.push(this.newFoodMorning)
      this.newFoodMorning.foodName = ''
    },
    removeFoodsMorning: function (foodMor) {
      firebase.database().ref('foodsMorning/' + foodMor.id).remove()
    },
    addFoodsAfternoon: function () {
      foodsAfternoon.push(this.newFoodAfternoon)
      this.newFoodAfternoon.foodName = ''
    },
    removeFoodsAfternoon: function (foodAfter) {
      firebase.database().ref('foodsAfternoon/' + foodAfter.id).remove()
    },
    addFoodsEvening: function () {
      foodsEvening.push(this.newFoodEvening)
      this.newFoodEvening.foodName = ''
    },
    removeFoodsEvening: function (foodEve) {
      firebase.database().ref('foodsEvening/' + foodEve.id).remove()
    },
    selectBlueHome () {
      this.homes = '1'
      this.statusManage = true
      this.statusUsers = true
      this.blueHomeCheck = false
      this.checkInBlue = false
      this.greenHomeCheck = false
      this.checkInGreen = false
      this.orangeHomeCheck = false
      this.checkInOrange = false
      this.pinkHomeCheck = false
      this.checkInPink = false
      this.countFoodCheck = true
      this.blueHomeRemoveCheck = false
      this.greenHomeRemoveCheck = false
      this.orangeHomeRemoveCheck = false
      this.pinkHomeRemoveCheck = false
      this.show = true
      this.newBlueUsers.name = ''
      this.newBlueUsers.idUser = ''
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.name = ''
      this.newGreenUsers.idUser = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.name = ''
      this.newOrangeUsers.idUser = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.name = ''
      this.newPinkUsers.idUser = ''
      this.newPinkUsers.idCard = ''
    },
    selectGreenHome () {
      this.homes = '2'
      this.statusManage = true
      this.statusUsers = true
      this.blueHomeCheck = false
      this.checkInBlue = false
      this.greenHomeCheck = false
      this.checkInGreen = false
      this.orangeHomeCheck = false
      this.checkInOrange = false
      this.pinkHomeCheck = false
      this.checkInPink = false
      this.countFoodCheck = true
      this.blueHomeRemoveCheck = false
      this.greenHomeRemoveCheck = false
      this.orangeHomeRemoveCheck = false
      this.pinkHomeRemoveCheck = false
      this.show = true
      this.newBlueUsers.name = ''
      this.newBlueUsers.idUser = ''
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.name = ''
      this.newGreenUsers.idUser = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.name = ''
      this.newOrangeUsers.idUser = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.name = ''
      this.newPinkUsers.idUser = ''
      this.newPinkUsers.idCard = ''
    },
    selectOrangeHome () {
      this.homes = '3'
      this.statusManage = true
      this.statusUsers = true
      this.blueHomeCheck = false
      this.checkInBlue = false
      this.greenHomeCheck = false
      this.checkInGreen = false
      this.orangeHomeCheck = false
      this.checkInOrange = false
      this.pinkHomeCheck = false
      this.checkInPink = false
      this.countFoodCheck = true
      this.blueHomeRemoveCheck = false
      this.greenHomeRemoveCheck = false
      this.orangeHomeRemoveCheck = false
      this.pinkHomeRemoveCheck = false
      this.show = true
      this.newBlueUsers.name = ''
      this.newBlueUsers.idUser = ''
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.name = ''
      this.newGreenUsers.idUser = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.name = ''
      this.newOrangeUsers.idUser = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.name = ''
      this.newPinkUsers.idUser = ''
      this.newPinkUsers.idCard = ''
    },
    selectPinkHome () {
      this.homes = '4'
      this.statusManage = true
      this.statusUsers = true
      this.blueHomeCheck = false
      this.checkInBlue = false
      this.greenHomeCheck = false
      this.checkInGreen = false
      this.orangeHomeCheck = false
      this.checkInOrange = false
      this.pinkHomeCheck = false
      this.checkInPink = false
      this.countFoodCheck = true
      this.blueHomeRemoveCheck = false
      this.greenHomeRemoveCheck = false
      this.orangeHomeRemoveCheck = false
      this.pinkHomeRemoveCheck = false
      this.show = true
      this.newBlueUsers.name = ''
      this.newBlueUsers.idUser = ''
      this.newBlueUsers.idCard = ''
      this.newGreenUsers.name = ''
      this.newGreenUsers.idUser = ''
      this.newGreenUsers.idCard = ''
      this.newOrangeUsers.name = ''
      this.newOrangeUsers.idUser = ''
      this.newOrangeUsers.idCard = ''
      this.newPinkUsers.name = ''
      this.newPinkUsers.idUser = ''
      this.newPinkUsers.idCard = ''
    },
    selectFoodsMorning (food, id, home) {
      var vm = this
      if (home === 'บ้านฟ้า') {
        firebase.database().ref('blueUsers/' + id).update({
          foodMorningName: vm.newBlueUsers.foodMorningName = food
        })
        this.editMorBlueTwo = true
      }
      if (home === 'บ้านเขียว') {
        firebase.database().ref('greenUsers/' + id).update({
          foodMorningName: vm.newGreenUsers.foodMorningName = food
        })
        this.editMorGreenTwo = true
      }
      if (home === 'บ้านส้ม') {
        firebase.database().ref('orangeUsers/' + id).update({
          foodMorningName: vm.newOrangeUsers.foodMorningName = food
        })
        this.editMorOrangeTwo = true
      }
      if (home === 'บ้านชมพู') {
        firebase.database().ref('pinkUsers/' + id).update({
          foodMorningName: vm.newPinkUsers.foodMorningName = food
        })
        this.editMorPinkTwo = true
      }
    },
    selectFoodsAfternoon (food, id, home) {
      var vm = this
      if (home === 'บ้านฟ้า') {
        firebase.database().ref('blueUsers/' + id).update({
          foodAfternoonName: vm.newBlueUsers.foodAfternoonName = food
        })
        this.editAfterBlueTwo = true
      }
      if (home === 'บ้านเขียว') {
        firebase.database().ref('greenUsers/' + id).update({
          foodAfternoonName: vm.newGreenUsers.foodAfternoonName = food
        })
        this.editAfterGreenTwo = true
      }
      if (home === 'บ้านส้ม') {
        firebase.database().ref('orangeUsers/' + id).update({
          foodAfternoonName: vm.newOrangeUsers.foodAfternoonName = food
        })
        this.editAfterOrangeTwo = true
      }
      if (home === 'บ้านชมพู') {
        firebase.database().ref('pinkUsers/' + id).update({
          foodAfternoonName: vm.newPinkUsers.foodAfternoonName = food
        })
        this.editAfterPinkTwo = true
      }
    },
    selectFoodsEvening (food, id, home) {
      var vm = this
      if (home === 'บ้านฟ้า') {
        firebase.database().ref('blueUsers/' + id).update({
          foodEveningName: vm.newBlueUsers.foodEveningName = food
        })
        this.editEveBlueTwo = true
      }
      if (home === 'บ้านเขียว') {
        firebase.database().ref('greenUsers/' + id).update({
          foodEveningName: vm.newGreenUsers.foodEveningName = food
        })
        this.editEveGreenTwo = true
      }
      if (home === 'บ้านส้ม') {
        firebase.database().ref('orangeUsers/' + id).update({
          foodEveningName: vm.newOrangeUsers.foodEveningName = food
        })
        this.editEveOrangeTwo = true
      }
      if (home === 'บ้านชมพู') {
        firebase.database().ref('pinkUsers/' + id).update({
          foodEveningName: vm.newPinkUsers.foodEveningName = food
        })
        this.editEvePinkTwo = true
      }
    },
    editFoodStaff (id, home) {
      var vm = this
      if (home === 'บ้านเขียว') {
        firebase.database().ref('greenUsers/' + id).update({
          foodMorningName: vm.newGreenUsers.foodMorningName = '',
          foodAfternoonName: vm.newGreenUsers.foodAfternoonName = '',
          foodEveningName: vm.newGreenUsers.foodEveningName = '',
          temp: vm.newGreenUsers.temp = true
        })
        this.checkShowMenuGreen = true
        this.clickNameGreen = true
        this.newGreenUsers.idCard = ''
      }
      if (home === 'บ้านฟ้า') {
        firebase.database().ref('blueUsers/' + id).update({
          foodMorningName: vm.newBlueUsers.foodMorningName = '',
          foodAfternoonName: vm.newBlueUsers.foodAfternoonName = '',
          foodEveningName: vm.newBlueUsers.foodEveningName = '',
          temp: vm.newBlueUsers.temp = true
        })
        this.checkShowMenuBlue = true
        this.clickNameBlue = true
        this.newBlueUsers.idCard = ''
      }
      if (home === 'บ้านส้ม') {
        firebase.database().ref('orangeUsers/' + id).update({
          foodMorningName: vm.newOrangeUsers.foodMorningName = '',
          foodAfternoonName: vm.newOrangeUsers.foodAfternoonName = '',
          foodEveningName: vm.newOrangeUsers.foodEveningName = '',
          temp: vm.newOrangeUsers.temp = true
        })
        this.checkShowMenuOrange = true
        this.clickNameOrange = true
        this.newOrangeUsers.idCard = ''
      }
      if (home === 'บ้านชมพู') {
        firebase.database().ref('pinkUsers/' + id).update({
          foodMorningName: vm.newPinkUsers.foodMorningName = '',
          foodAfternoonName: vm.newPinkUsers.foodAfternoonName = '',
          foodEveningName: vm.newPinkUsers.foodEveningName = '',
          temp: vm.newPinkUsers.temp = true
        })
        this.checkShowMenuPink = true
        this.clickNamePink = true
        this.newPinkUsers.idCard = ''
      }
    },
    editFood (id, idCard) {
      var vm = this
      if (idCard === this.newGreenUsers.idCard) {
        firebase.database().ref('greenUsers/' + id).update({
          foodMorningName: vm.newGreenUsers.foodMorningName = '',
          foodAfternoonName: vm.newGreenUsers.foodAfternoonName = '',
          foodEveningName: vm.newGreenUsers.foodEveningName = '',
          temp: vm.newGreenUsers.temp = true
        })
        this.checkShowMenuGreen = true
        this.clickNameGreen = true
        this.newGreenUsers.idCard = ''
      }
      if (idCard === this.newBlueUsers.idCard) {
        firebase.database().ref('blueUsers/' + id).update({
          foodMorningName: vm.newBlueUsers.foodMorningName = '',
          foodAfternoonName: vm.newBlueUsers.foodAfternoonName = '',
          foodEveningName: vm.newBlueUsers.foodEveningName = '',
          temp: vm.newBlueUsers.temp = true
        })
        this.checkShowMenuBlue = true
        this.clickNameBlue = true
        this.newBlueUsers.idCard = ''
      }
      if (idCard === this.newOrangeUsers.idCard) {
        firebase.database().ref('orangeUsers/' + id).update({
          foodMorningName: vm.newOrangeUsers.foodMorningName = '',
          foodAfternoonName: vm.newOrangeUsers.foodAfternoonName = '',
          foodEveningName: vm.newOrangeUsers.foodEveningName = '',
          temp: vm.newOrangeUsers.temp = true
        })
        this.checkShowMenuOrange = true
        this.clickNameOrange = true
        this.newOrangeUsers.idCard = ''
      }
      if (idCard === this.newPinkUsers.idCard) {
        firebase.database().ref('pinkUsers/' + id).update({
          foodMorningName: vm.newPinkUsers.foodMorningName = '',
          foodAfternoonName: vm.newPinkUsers.foodAfternoonName = '',
          foodEveningName: vm.newPinkUsers.foodEveningName = '',
          temp: vm.newPinkUsers.temp = true
        })
        this.checkShowMenuPink = true
        this.clickNamePink = true
        this.newPinkUsers.idCard = ''
      }
    },
    edit (id, home, idCard) {
      if (home === 'บ้านฟ้า') {
        this.clickNameBlue = false
        this.checkShowMenuBlue = false
        this.showEditButton = true
        this.showEditButton2 = true
        this.ei = false
        this.ei2 = true
      }
      if (home === 'บ้านเขียว') {
        this.clickNameGreen = false
        this.checkShowMenuGreen = false
        this.showEditButton = true
        this.showEditButton2 = true
        this.ei = false
        this.ei2 = true
      }
      if (home === 'บ้านส้ม') {
        this.clickNameOrange = false
        this.checkShowMenuOrange = false
        this.showEditButton = true
        this.showEditButton2 = true
        this.ei = false
        this.ei2 = true
      }
      if (home === 'บ้านชมพู') {
        this.clickNamePink = false
        this.checkShowMenuPink = false
        this.showEditButton = true
        this.showEditButton2 = true
        this.ei = false
        this.ei2 = true
      }
    }
  },
  computed: {
    countFoodBlue: function () {
      var count = {
        Morning: {
          m1: 0,
          m2: 0,
          m3: 0
        },
        Afternoon: {
          m1: 0,
          m2: 0,
          m3: 0
        },
        Evening: {
          m1: 0,
          m2: 0,
          m3: 0
        }
      }
      for (var a = 0; a < this.blueUsers.length; a++) {
        for (var b = 0; b < this.foodsMorning.length; b++) {
          if (this.blueUsers[a].foodMorningName === this.foodsMorning[b].foodName) {
            if (b === 0) {
              count.Morning.m1 ++
            }
            if (b === 1) {
              count.Morning.m2 ++
            }
            if (b === 2) {
              count.Morning.m3 ++
            }
          }
        }
      }

      for (var c = 0; c < this.blueUsers.length; c++) {
        for (var d = 0; d < this.foodsAfternoon.length; d++) {
          if (this.blueUsers[c].foodAfternoonName === this.foodsAfternoon[d].foodName) {
            if (d === 0) {
              count.Afternoon.m1 ++
            }
            if (d === 1) {
              count.Afternoon.m2 ++
            }
            if (d === 2) {
              count.Afternoon.m3 ++
            }
          }
        }
      }

      for (var e = 0; e < this.blueUsers.length; e++) {
        for (var f = 0; f < this.foodsEvening.length; f++) {
          if (this.blueUsers[e].foodEveningName === this.foodsEvening[f].foodName) {
            if (f === 0) {
              count.Evening.m1 ++
            }
            if (f === 1) {
              count.Evening.m2 ++
            }
            if (f === 2) {
              count.Evening.m3 ++
            }
          }
        }
      }

      return count
    },
    countFoodGreen: function () {
      var count = {
        Morning: {
          m1: 0,
          m2: 0,
          m3: 0
        },
        Afternoon: {
          m1: 0,
          m2: 0,
          m3: 0
        },
        Evening: {
          m1: 0,
          m2: 0,
          m3: 0
        }
      }
      for (var a = 0; a < this.greenUsers.length; a++) {
        for (var b = 0; b < this.foodsMorning.length; b++) {
          if (this.greenUsers[a].foodMorningName === this.foodsMorning[b].foodName) {
            if (b === 0) {
              count.Morning.m1 ++
            }
            if (b === 1) {
              count.Morning.m2 ++
            }
            if (b === 2) {
              count.Morning.m3 ++
            }
          }
        }
      }

      for (var c = 0; c < this.greenUsers.length; c++) {
        for (var d = 0; d < this.foodsAfternoon.length; d++) {
          if (this.greenUsers[c].foodAfternoonName === this.foodsAfternoon[d].foodName) {
            if (d === 0) {
              count.Afternoon.m1 ++
            }
            if (d === 1) {
              count.Afternoon.m2 ++
            }
            if (d === 2) {
              count.Afternoon.m3 ++
            }
          }
        }
      }

      for (var e = 0; e < this.greenUsers.length; e++) {
        for (var f = 0; f < this.foodsEvening.length; f++) {
          if (this.greenUsers[e].foodEveningName === this.foodsEvening[f].foodName) {
            if (f === 0) {
              count.Evening.m1 ++
            }
            if (f === 1) {
              count.Evening.m2 ++
            }
            if (f === 2) {
              count.Evening.m3 ++
            }
          }
        }
      }

      return count
    },
    countFoodOrange: function () {
      var count = {
        Morning: {
          m1: 0,
          m2: 0,
          m3: 0
        },
        Afternoon: {
          m1: 0,
          m2: 0,
          m3: 0
        },
        Evening: {
          m1: 0,
          m2: 0,
          m3: 0
        }
      }
      for (var a = 0; a < this.orangeUsers.length; a++) {
        for (var b = 0; b < this.foodsMorning.length; b++) {
          if (this.orangeUsers[a].foodMorningName === this.foodsMorning[b].foodName) {
            if (b === 0) {
              count.Morning.m1 ++
            }
            if (b === 1) {
              count.Morning.m2 ++
            }
            if (b === 2) {
              count.Morning.m3 ++
            }
          }
        }
      }

      for (var c = 0; c < this.orangeUsers.length; c++) {
        for (var d = 0; d < this.foodsAfternoon.length; d++) {
          if (this.orangeUsers[c].foodAfternoonName === this.foodsAfternoon[d].foodName) {
            if (d === 0) {
              count.Afternoon.m1 ++
            }
            if (d === 1) {
              count.Afternoon.m2 ++
            }
            if (d === 2) {
              count.Afternoon.m3 ++
            }
          }
        }
      }

      for (var e = 0; e < this.orangeUsers.length; e++) {
        for (var f = 0; f < this.foodsEvening.length; f++) {
          if (this.orangeUsers[e].foodEveningName === this.foodsEvening[f].foodName) {
            if (f === 0) {
              count.Evening.m1 ++
            }
            if (f === 1) {
              count.Evening.m2 ++
            }
            if (f === 2) {
              count.Evening.m3 ++
            }
          }
        }
      }

      return count
    },
    countFoodPink: function () {
      var count = {
        Morning: {
          m1: 0,
          m2: 0,
          m3: 0
        },
        Afternoon: {
          m1: 0,
          m2: 0,
          m3: 0
        },
        Evening: {
          m1: 0,
          m2: 0,
          m3: 0
        }
      }
      for (var a = 0; a < this.pinkUsers.length; a++) {
        for (var b = 0; b < this.foodsMorning.length; b++) {
          if (this.pinkUsers[a].foodMorningName === this.foodsMorning[b].foodName) {
            if (b === 0) {
              count.Morning.m1 ++
            }
            if (b === 1) {
              count.Morning.m2 ++
            }
            if (b === 2) {
              count.Morning.m3 ++
            }
          }
        }
      }

      for (var c = 0; c < this.pinkUsers.length; c++) {
        for (var d = 0; d < this.foodsAfternoon.length; d++) {
          if (this.pinkUsers[c].foodAfternoonName === this.foodsAfternoon[d].foodName) {
            if (d === 0) {
              count.Afternoon.m1 ++
            }
            if (d === 1) {
              count.Afternoon.m2 ++
            }
            if (d === 2) {
              count.Afternoon.m3 ++
            }
          }
        }
      }

      for (var e = 0; e < this.pinkUsers.length; e++) {
        for (var f = 0; f < this.foodsEvening.length; f++) {
          if (this.pinkUsers[e].foodEveningName === this.foodsEvening[f].foodName) {
            if (f === 0) {
              count.Evening.m1 ++
            }
            if (f === 1) {
              count.Evening.m2 ++
            }
            if (f === 2) {
              count.Evening.m3 ++
            }
          }
        }
      }

      return count
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Prompt&subset=thai');
.font{
font-family: 'Prompt', sans-serif;
}
.color{
  color: white;
  font-size: 17px;
}
.floorback{
background-image:url('./bg.jpg');
}
.head{
  margin-left: -49%;
  width: 98%;
  height: 40px;
  display: inline-block;
  background:#C25B56;
  padding: 10px;
  box-shadow: 0 0 5px #000;
  z-index: 999;
  position: fixed;
}
</style>
