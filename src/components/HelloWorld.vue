<template>
  <div class="text-center">
    <h1>
      Gerador de Nomes
      <span class="fa fa-check"></span>
    </h1>
    <h6 class="text-secondary">Utilizando o VUEJS</h6>
  </div>
  <div id="main">
    <div class="container">
      <div class="row">
        <div class="col-md">
          <h5>
            Prefixos
            <span class="badge badge-info">{{ prefixes.length }}</span>
          </h5>
          <div class="card">
            <div class="card-body">
              <ul class="list-group">
                <li class="list-group-item" v-for="prefix in prefixes" v-bind:key="prefix">
                  <div class="row">
                    <div class="col-md">{{ prefix }}</div>
                    <div class="col-md text-right">
                      <button class="btn btn-danger" v-on:click="deletePrefix(prefix)">
                        <span class="fa fa-trash"></span>
                      </button>
                    </div>
                  </div>
                </li>
              </ul>
              <br />

              <div class="input-group">
                <input
                  type="text"
                  class="form-control"
                  v-model="prefix"
                  placeholder="Digite o prefixo"
                  v-on:keyup.enter="addprefix(prefix)"
                />
                <div class="input-group-append">
                  <button class="btn btn-info" v-on:click="addprefix(prefix)">
                    <span class="fa fa-plus"></span>
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-md">
          <h5>
            Sufixos
            <span class="badge badge-info">{{ sufixes.length }}</span>
          </h5>

          <div class="card">
            <div class="card-body">
              <ul class="list-group">
                <li class="list-group-item" v-for="sufix in sufixes" v-bind:key="sufix">
                  <div class="row">
                    <div class="col-md">{{ sufix }}</div>
                    <div class="col-md text-right">
                      <button class="btn btn-danger" v-on:click="deleteSufix(sufix)">
                        <span class="fa fa-trash"></span>
                      </button>
                    </div>
                  </div>
                </li>
              </ul>
              <br />
              <div class="input-group">
                <input
                  type="text"
                  class="form-control"
                  v-model="sufix"
                  placeholder="Digite o sufixo"
                  v-on:keyup.enter="addsufix(sufix)"
                />
                <div class="input-group-append">
                  <button class="btn btn-info" v-on:click="addsufix(sufix)">
                    <span class="fa fa-plus"></span>
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <br />
      <h5>
        Domínios
        <span class="badge badge-info">{{domains.length}}</span>
      </h5>
      <div class="card">
        <div class="card-body">
          <ul class="list-group">
            <li class="list-group-item" v-for="domain in domains" v-bind:key="domain">{{domain}}</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";

export default {
	name: "app",
	data: () => {
		return {
			prefixes: [],
			sufixes: [],
			domains: [],
		};
	},
	methods: {
		addprefix(prefix) {
			this.prefixes.push(prefix);
			this.prefix = "";
			this.generate();
		},
		addsufix(sufix) {
			this.sufixes.push(sufix);
			this.sufix = "";
			this.generate();
		},

		generate() {
			this.domains = [];
			for (const prefix of this.prefixes) {
				for (const sufix of this.sufixes) {
					this.domains.push(prefix + sufix);
				}
			}
		},

		deletePrefix(prefix) {
			this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
			this.generate();
      
		},
		deleteSufix(sufix) {
			this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
			this.generate();
      
		},
	},
};
</script>

<style>
#main {
  background-color: #f1f1f1;
  padding-top: 30px;
  padding-bottom: 30px;
}
</style>
