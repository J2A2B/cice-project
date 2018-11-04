<template>
  <div class="container-cice">
    <h1>Le convertisseur de <span>CICE</span></h1>
    <table>
      <caption>Prévision des effets budgétaires du CICE (en milliards d'eauros)
          [<a href="https://www.liberation.fr/checknews/2018/06/08/combien-l-etat-va-t-il-verser-aux-entreprises-avec-le-cice-en-2018_1657300" target="_blank">source</a>]
      </caption>
        <caption>Total : {{calcGlobalAmountCice}} Milliards d'euros</caption>
      <tr>
        <th v-for="val in ciceYears">{{val.year}}</th>
      </tr>
      <tr>
        <td v-for="val in ciceYears">{{val.amount}}</td>
      </tr>
    </table>
    <p>Indiquez le type d'emploi et le salaire brut annuel</p>
      <input
              placeholder="type d'emploi"
              type="text"
              v-model="jobType"
              required/>
    <input
            placeholder="salaire brut annuel"
            type="number"
            @change="changeAnnualSalary($event)"
            required/>
      <h2>
          Le pacte CICE pourrait créer
          <span>{{this.createdJobs}}</span>
          emplois de
          <span>{{this.jobType}}</span>
          sur la période de 2014 à 2020 à <span>
          {{this.grossAnnualSalary}}€
          </span> brut par an
      </h2>
      <iframe
              width="660" height="415"
              src="https://www.youtube.com/embed/2UyaNPzu4W4"
              frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
              allowfullscreen>
      </iframe>
      <ul class="story-modal-social">
          <li>
              <a href="#" @click.prevent @click="socialShare('twitter')">
                  <div class="cont-img">
                      <div class="img-twit"></div>
                      <span>share</span>
                  </div>
              </a>
          </li>
          <li>
              <a href="#" @click.prevent @click="socialShare('facebook')">
                  <div class="cont-img">
                      <div class="img-fb"></div>
                      <span>share</span>
                  </div>
              </a>
          </li>
          <li>
              <a href="#" @click.prevent @click="socialShare('linkedin')">
                  <div class="cont-img">
                      <div class="img-link"></div>
                      <span>share</span>
                  </div>
              </a>
          </li>
      </ul>
      <span>{{this.errorMsg}}</span>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
    data: () => ({
        createdJobs: 0,
        grossAnnualSalary: 0,
        jobType: '',
        fullPhrase: '',
        globalAmoutCice: 0,
        errorMsg: '',
        ciceYears: [
            {
                year: 2014,
                amount: 6.6,
            },
            {
                year: 2015,
                amount: 12.5,
            },
            {
                year: 2016,
                amount: 12.9,
            },
            {
                year: 2017,
                amount: 16.5,
            },
            {
                year: 2018,
                amount: 21,
            },
            {
                year: 2019,
                amount: 19.6,
            },
            {
                year: 2020,
                amount: 10.2,
            },
        ]
    }),
    computed: {
        calcGlobalAmountCice(){
            let amountList = this.ciceYears.map(val => val.amount)
            return this.globalAmoutCice = amountList.reduce((a, b) => a + b, 0);
        }
    },
    methods: {
        changeAnnualSalary(value){
            const globalAmoutCice = 99000000000
            const grossAnnualSalary = value.target.value
            this.createdJobs = Math.round(((globalAmoutCice/(grossAnnualSalary*7)))).toLocaleString()
            this.grossAnnualSalary = (grossAnnualSalary/1).toLocaleString()
            this.fullPhrase = 'Le pacte CICE pourrait créer ' + this.createdJobs + 'emplois de ' + this.jobType + ' sur la période de 2014 à 2020, à ' + this.grossAnnualSalary + ' brut par an'
        },
        socialShare: function (name) {
            if (this.fullPhrase.length > 0) {
                this.errorMsg = ''
                let url = encodeURIComponent(window.location.href.replace('#', ''))
                let text = ''

                if (name === 'facebook') {
                    window.open('https://www.facebook.com/sharer/sharer.php?u=' + url, '', 'width=626,height=436')
                } else if (name === 'twitter') {
                    text = encodeURIComponent(this.fullPhrase)
                    console.log(text)
                    window.open('https://twitter.com/share?url=' + url + '&text=' + text, '', 'width=626,height=436')
                } else if (name === 'linkedin') {
                    text = encodeURIComponent(this.fullPhrase)
                    window.open('https://www.linkedin.com/shareArticle?mini=true&url=' + url + '&text=' + text, '', 'width=626,height=436')
                }
            } else {
                this.errorMsg = 'Vous devez renseigner les champs avant de partager :)'
            }
        },
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .container-cice{
    padding: 20px;
    border: 10px solid #e61e49;
    border-radius: 3px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 60vw;
      color: #262626;
  }
  h1{
      font-size: 3.25em;
      letter-spacing: .05em;
  }
  h2 {
      width: 900px;
  }
  h1 span{
      color: lightskyblue;
  }
  h2 span:first-child {
      color:#e61e49;
  }
  h2 span:nth-child(2) {
      color: lightskyblue;
  }
  h2 span:nth-child(3) {
      color:#dc9930;
  }
  input {
    height: 30px;
    width: 150px;
      border-radius: 3px;
      margin-top: 10px;
  }
  table
  {
      border-collapse: collapse;
  }
  caption{
      margin-bottom: 10px;
  }
  td, th /* Mettre une bordure sur les td ET les th */
  {
      border: 1px solid lightskyblue;
      border-radius: 3px;
      padding: 5px;
  }
  a{
      text-decoration: none;
      color: lightskyblue;
  }
    .story-modal-social {
        display: flex;
        margin-top: 40px;
    }
    li {
        list-style: none;
        border: 2px solid lightskyblue;
        border-radius: 3px;
        margin-right: 15px;
    }
    li a {
        color: #262626;
    }
    .cont-img {
        margin: 5px;
        display: flex;
        justify-content: space-around;
        align-items: center;
    }
    .cont-img .img-twit {
        height: 20px;
        width: 20px;
        background: url(../assets/twitter-logo.png) no-repeat center;
        background-size: cover;
    }
  .cont-img .img-fb {
      height: 20px;
      width: 20px;
      background: url(../assets/logo-fb.png) no-repeat center;
      background-size: cover;
  }
  .cont-img .img-link {
      height: 20px;
      width: 20px;
      background: url(../assets/linkedin-logo.jpg) no-repeat center;
      background-size: cover;
  }
    .cont-img span {
        margin-left: 5px;
    }
</style>
