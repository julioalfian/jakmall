<template>
  <div id="app">
    <!--<div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>-->
    <router-view />
  </div>
</template>

<style lang="stylus">
@import './assets/style/variable.styl';
@font-face
  font-family Inter
  font-style normal
  src url(./assets/fonts/Inter-Regular.ttf)
@font-face
  font-family Inter-Medium
  font-style normal
  src url(./assets/fonts/Inter-Medium.ttf)
@font-face
  font-family Montserrat
  font-style normal
  src url(./assets/fonts/Montserrat-Regular.ttf)
@font-face
  font-family Montserrat-Bold
  font-style normal
  src url(./assets/fonts/Montserrat-Bold.ttf)

body
  font-family Inter
  font-weight 500
  font-size 16px
  color color-black
  background color-orange-bg
  @media screen and (max-width: 768px)
    font-size 14px
  h1, h2, h3, h4, h5, h6
    font-family: Montserrat-Bold
    color: color-orange
    margin 0
  h1
    font-size: 36px
    line-height: 44px
    position : relative
    z-index : 2
    &:after
      z-index : -1
      position : absolute
      width : 300px
      height : 8px
      background : color-gray-2
      content : ''
      bottom : 4px
      left : 0
    @media screen and (max-width: 768px)
      font-size: 24px
      line-height: 32px
      &:after
        width : 180px

  h3
    font-size: 24px
    line-height: 29px
    @media screen and (max-width: 768px)
      font-size: 18px
      line-height: 24px
  a
    text-decoration: none
  .container
    margin: 0 auto
    @media screen and (min-width: 1200px)
      max-width: 1100px
    @media screen and (min-width: 993px) and (max-width: 1200px)
      max-width: 960px
      margin : 0 auto
    @media screen and (min-width: 769px) and (max-width: 992px)
      max-width: 720px
      margin : 0 auto
    @media screen and (max-width: 768px)
      max-width: 100%
      margin : 0 15px

  input:disabled
    background-color : rgba(118, 118, 118, 0.2);
  
  .mb-30
    margin-bottom : 30px
  .mb-60
    margin-bottom : 60px
  .height-100
    height : 100%
  .align-center
    align-items : center
  .justify-center
    justify-content : center
  .flex-wrap
    flex-wrap : wrap
  .divider
    background: #D8D8D8;
    height : 1px
    width : 80px
    margin : 21px 0
  .errorText
    font-size : 12px
    color : red
    font-style : italic

  .form-group
    position : relative
    margin-bottom 10px
    &.active
      .form-group__label
        top : 10px
        font-size : 13px
        opacity : .8
      .form-group__input
        padding-bottom : 11px
        padding-top : 29px
    &.valid
      &:after
        content : '\2713'
        font-size : 20px
        position : absolute
        right : 20px
        top : 30%
        color : color-green
      .form-group__label
        color : color-green
      .form-group__input 
        &:focus
          outline-color : color-green
      
    &.error
      &:after
        content : '\00d7'
        font-size : 20px
        position : absolute
        right : 20px
        top : 30%
        color : color-orange
      .form-group__label
        color : color-orange
      .form-group__input 
        &:focus
          outline-color : color-orange
  .form-group__label
    transition : .3s
    left: 15px
    top : 20px
    position: absolute
    color : color-black
    opacity : 0
    line-height: 19px
    display : none
    &.active
      display : block
      top : 10px !important
      color : color-gray
      font-size : 13px
      opacity : .8
  .form-group__input
    z-index : 1
    font-size : 16px
    color : color-black
    font-weight : bold
    border 0
    border 1px solid color-gray
    padding : 20px 15px
    width : calc(100% - 30px)
    outline-color : color-gray
    &::placeholder
      color : color-black
      opacity : .4
    &::-ms-input-placeholder
      color : color-black
      opacity : .4
    &::-ms-input-placeholder
      color : color-black
      opacity : .4
    &.active
      padding-bottom : 11px
      padding-top : 29px
    &.valid
      outline-color : color-green
    &.error
      outline-color : color-orange
  .form-group__input--height
    height : 120px
    font-family : Inter
    font-weight : bold
    &::placeholder
      color : color-black
      opacity : .4
    &::-ms-input-placeholder
      color : color-black
      opacity : .4
    &::-ms-input-placeholder
      color : color-black
      opacity : .4
  .checkmark
    display : flex
    align-items : center
    cursor : pointer
    @media screen and (max-width: 767px)
      margin-top : 12px
    input[type="checkbox"]:checked + span::after 
      content: '';
      position: absolute;
      width: 1.2ex;
      height: 0.4ex;
      background: rgba(0, 0, 0, 0);
      top: 7px;
      left: 5px;
      border: 3px solid color-green;
      border-top: none;
      border-right: none;
      -webkit-transform: rotate(-45deg);
      -moz-transform: rotate(-45deg);
      -o-transform: rotate(-45deg);
      -ms-transform: rotate(-45deg);
      transform: rotate(-45deg);

    input[type="checkbox"] 
      line-height: 2.1ex;

    input[type="checkbox"] 
        position: absolute;
        left: -999em;

    input[type="checkbox"] + span 
        position: relative;
        overflow: hidden;
        cursor: pointer;

    input[type="checkbox"] + span::before 
      content: "";
      display: inline-block;
      vertical-align: -33%;
      height: 18px;
      width: 18px;
      background-color: white;
      border: 2px solid color-gray;
      margin-right: 10px;

    input[type="checkbox"]:checked + span::before
      border: 2px solid color-green;
    span
      font-family : Inter
      font-weight : 500
      color : color-black
      font-size: 14px
      opacity : .8
  .required
    display : block
    margin-top : -5px
    margin-bottom : 10px
    font-size : 12px
    color : red

  .form-select
    margin-right : 10px
    position : relative
  .form-group__input-radio
    display : none
  .form-group__label-radio
    display : flex
    justify-content : center
    flex-direction : column
    width : 180px
    height : 60px
    border : 1px solid color-gray
    cursor : pointer
    @media screen and (max-width: 768px)
      width : 160px
    @media screen and (max-width: 576px)
      width : 130px
    .text
      margin : 0 15px
      font-size : 13px
      line-height : 16px
      color : black
      opacity : .6
      transition : .3s
      &.big
        font-size : 16px
    .price
      margin : 0 15px
      font-weight: bold
      font-size: 16px
      line-height: 19px
      color : color-black
      opacity : .6
      transition : .3s
  .form-select
    input[type=radio]:checked + label
      background: rgba(27, 217, 123, 0.1);
      border : 2px solid color-green
      &:after
        content : '\2713'
        font-size : 20px
        position : absolute
        right : 20px
        top : 30%
        color : color-green
      .text
      .price
        opacity : 1

</style>
