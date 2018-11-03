<template>
  <div class="container-cice">
    <h1>Le convertisseur de <span>CICE</span></h1>
    <table>
      <caption>Prévision des effets budgétaires du CICE (en milliards d'eauros) [<a href="https://www.liberation.fr/checknews/2018/06/08/combien-l-etat-va-t-il-verser-aux-entreprises-avec-le-cice-en-2018_1657300" target="_blank">source</a>]</caption>
        <caption>Total : 99,3 Milliards d'euros</caption>
      <tr>
        <th>2014</th>
        <th>2015</th>
        <th>2016</th>
        <th>2017</th>
        <th>2018</th>
        <th>2019</th>
        <th>2020</th>
      </tr>
      <tr>
        <td>6,6</td>
        <td>12,5</td>
        <td>12,9</td>
        <td>16,5</td>
        <td>21,0</td>
        <td>19,6</td>
        <td>10,2</td>
      </tr>
    </table>
    <p>Indiquez le salaire brut annuel</p>
      <input
              placeholder="type d'emploi"
              type="text"
              v-model="jobType"
      />
    <input
            placeholder="salaire brut annuel"
            type="number"
            @change="changeAnnualSalary($event)"/>
      <h2>Le pacte CICE pourrait créer <span>{{this.createdJobs}}</span> {{this.jobType}} en 7ans à <span>{{this.grossAnnualSalary}}€</span> but par an</h2>
      <iframe width="660" height="415" src="https://www.youtube.com/embed/2UyaNPzu4W4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
      <p></p>
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
    }),
    methods: {
        changeAnnualSalary(value){
            const globalAmoutCice = 99000000000
            const grossAnnualSalary = value.target.value
            this.createdJobs = ((globalAmoutCice/grossAnnualSalary)/7).toLocaleString()
            this.grossAnnualSalary = (grossAnnualSalary/1).toLocaleString()
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .container-cice{
    padding: 20px;
    border: 10px solid #e61e49;
    background: #333333;
    border-radius: 3px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 60vw;
      color: white;
  }
  h1{
      font-size: 3.25em;
      letter-spacing: .05em;
  }
  h1 span{
      color: lightskyblue;
  }
  h2 span:first-child {
      color:#e61e49;
  }
  h2 span:nth-child(2) {
      color:#dc9930;
  }
  input {
    height: 30px;
    width: 150px;
      border-radius: 3px;
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
</style>
