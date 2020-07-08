<template>
  <div>
    <div
      class="modal fade"
      id="exampleModal"
      aria-labelledby="exampleModalLabel"
      tabindex="-1"
      role="dialog"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-lg">
        <div class="modal-content tamaño">
          <div class="modal-header header-modal text-light text-center">
            <div class="imagen">
              <img
                src="@/assets/adidas.png"
                alt
                class="rounded-circle"
                style="width: 50px;height: 50px;"
              />
            </div>
            <p class="mb-0 ml-auto">Añadir pregunta</p>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="row justify-content-center pt-5">
              <div class="Esq_input_pregunta">
                <p class="mb-0 text-muted text_question" style="z-index:2;">Pregunta</p>
                <el-input
                  aria-placeholder="Please input"
                  v-model="pregunta"
                  size="small"
                  class="h-100 w-100"
                ></el-input>
              </div>
            </div>
            <!-- El select -->
            <div class="row preguntas">
              <el-select v-model="value1" placeholder="Tipo de Respuesta" size="medium">
                <el-option
                  v-for="item in options1"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value"
                ></el-option>
              </el-select>
            </div>
            <!-- El select -->
            <!-- Respuestas -->
            <div class="respuestas_TipoListado pt-2" v-if="value1 == this.Valores">
              <div class="d-flex input_agregar_respuestas text-light">
                <button class="btn p-0 agregar_respuestas" @click="AgregarRespuestas">
                  Añadir respuestas
                  <span>
                    <i class="fas fa-plus"></i>
                  </span>
                </button>
              </div>
              <!-- Esto es el dragable -->
              <draggable :list="Respuestas" handle=".handle">
                <div class="row Lista_Valores" v-for="(list, idx) in Respuestas" :key="list.index">
                  <div class="col-auto text-muted">
                    <span>
                      <i class="fas fa-grip-lines handle"></i>
                    </span>
                  </div>
                  <div class="col-auto text-muted">Rta {{ list.index}} </div>
                  <div class="col-md-6">
                    <div class="Input_Respuesta">
                      <p
                        class="mb-0 Respuesta text-muted"
                        style="font-size: 15px;"
                      >Escribir una respuesta</p>
                    </div>
                    <el-input v-model="list.Respuesta_lista_modal"></el-input>
                  </div>
                  <div class="col-auto">
                    <button class="btn rounded-circle" @click="QuitarRespuesta(idx)">
                      <span>
                        <i class="fas fa-times"></i>
                      </span>
                    </button>
                  </div>
                </div>
              </draggable>
              <!-- Esto es el dragable -->
            </div>
            <div class="respuestas_texto row mt-2" v-if="value1 == this.Texto">
              <div class="col-auto text-muted">Ingresar maximo de caracteres</div>
              <div class="col-auto">
                <div class="input_caracteres">
                  <el-input v-model="caracteres"></el-input>
                </div>
              </div>
            </div>
            <div class="respuesta_rango" v-if="value1 == this.Rango">
              <div class="row">
                <div class="col-auto text-muted">Selecciona unidad de medida</div>
                <div class="col-auto">
                  <el-select v-model="value" placeholder="Select" size="medium">
                    <el-option
                      v-for="item in options"
                      :key="item.value"
                      :label="item.label"
                      :value="item.value"
                    ></el-option>
                  </el-select>
                </div>
              </div>
            </div>
            <!-- Respuestas -->
          </div>
          <div class="modal-footer d-flex justify-content-center">
            <button type="button" class="btn cancelar_pregunta p-1" data-dismiss="modal">Cancelar</button>
            <button type="button" class="btn aceptar_pregunta p-1">Siguiente</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
export default {
  components: {
    draggable
  },
  data() {
    return {
      Respuesta_lista_modal : '',
      caracteres: "",
      pregunta: "",
      value1: "",
      Valores: "Tipo lista de valores",
      Hora: "Tipo hora",
      Texto: "Tipo de texto",
      Rango: "Tipo rango",
      Archivo: "Tipo Archivo",
      options1: [
        {
          value: "Tipo lista de valores",
          label: "Tipo lista de valores"
        },
        {
          value: "Tipo hora",
          label: "Tipo hora"
        },
        {
          value: "Tipo de texto",
          label: "Tipo de texto"
        },
        {
          value: "Tipo rango",
          label: "Tipo rango"
        },
        {
          value: "Tipo Archivo",
          label: "Tipo Archivo"
        }
      ],
      options: [
        {
          value: "Option1",
          label: "Option1"
        },
        {
          value: "Option2",
          label: "Option2"
        },
        {
          value: "Option3",
          label: "Option3"
        },
        {
          value: "Option4",
          label: "Option4"
        },
        {
          value: "Option5",
          label: "Option5"
        }
      ],
      value: "",
      index: 1,
      Respuestas: [
        {
          index: 1,
          Respuesta_lista_modal: ""
        }
      ]
    };
  },
  methods :{
    AgregarRespuestas(){
      this.index++;
      this.Respuestas.push({
        index: this.index,
        Respuesta_lista_modal : ''
      })
    },
    QuitarRespuesta(idx){
      this.Respuestas.splice(idx,1);
    }
  }
};
</script>

<style lang="scss" scope>
.tamaño {
  min-height: 496px;
}

.respuestas_texto {
  padding-left: 90px;
}

.input_caracteres {
  width: 70px;
  height: 40px;
}

.aceptar_pregunta {
  background-color: #32a3fd;
  color: white;
  width: 110px;
  height: 32px;
}

.cancelar_pregunta {
  background-color: #bcbcbc;
  color: white;
  width: 110px;
  height: 32px;
}

.respuesta_rango {
  padding-left: 90px;
}

.Respuesta {
  position: absolute;
  top: -12px;
  right: 123px;
  z-index: 2;
}

.Input_Respuesta {
  position: relative;
}

.Lista_Valores {
  padding-left: 100px;
  padding-top: 20px;
}

.agregar_respuestas {
  border-radius: 20px;
  width: 200px;
  /* height: 80px; */
  background-color: #32a3fd;
  box-shadow: 0px 3px 6px #006ec53f;
}

.input_agregar_respuestas {
  padding-left: 85px;
}
.preguntas {
  padding-left: 106px;
  padding-top: 15px;
}

.text_question {
  position: absolute;
  left: 15px;
  top: -14px;
}

.Esq_input_pregunta {
  position: relative;
  border: solid;
  border-color: #e8e8e8;
  border-width: 1px;
  width: 515px;
  height: 29px;
}

.header-modal {
  width: 727px;
  height: 78px;
  background-color: teal;
  box-shadow: 0px 3px 9px #0000004f;
  border-radius: 0 0 23% 23%;
}

.modal-lg {
  width: 727px !important;
}
</style>
