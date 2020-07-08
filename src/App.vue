<template>
  <div id="app">
    <div id="header" class="header container-fluid">
      <div class="row">
        <div class="col-auto">
          <img
            src="@/assets/adidas.png"
            class="rounded-circle"
            style="width:50px;height:50px;box-shadow:0px 3px 6px #00000029"
            alt=""
          />
        </div>
        <div
          class="col-auto p-2"
          style="margin-left: 550px;color:#1F1B62;font-weight:bold;"
        >Configurar calidad</div>
        <div class="col-auto ml-auto">
          <el-dropdown trigger="click">
            <img
              src="@/assets/images.png"
              class="rounded-circle"
              style="width: 650x;height:50px;"
              alt
            />
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>Action 1</el-dropdown-item>
              <el-dropdown-item>Action 2</el-dropdown-item>
              <el-dropdown-item>Action 3</el-dropdown-item>
              <el-dropdown-item>Action 4</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </div>
        <div class="col-auto">
          <el-dropdown trigger="click">
            <img
              src="@/assets/images.png"
              class="rounded-circle"
              style="height: 50px;width:50px;"
              alt
            />
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>Action 1</el-dropdown-item>
              <el-dropdown-item>Action 2</el-dropdown-item>
              <el-dropdown-item>Action 3</el-dropdown-item>
              <el-dropdown-item>Action 4</el-dropdown-item>
              <el-dropdown-item>Action 5</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </div>
      </div>
    </div>
    <div class="contenedor-calidad p-3 my-3 mx-3">
      <el-tabs>
        <el-tab-pane label="Banco de preguntas Calidad" name="first">
          <div class="contenedor_matriz">
            <div class="row">
              <div
                class="col-md-2 text-center"
                style="font-size:18px;color: #1F1B62;"
              >Banco de preguntas</div>
              <div class="col-md-8 h-75 mt-3 separador_calidad_preguntas">
                <!-- Este es el separador -->
              </div>
              <div class="col-md-2 text-center p-1">
                <button
                  class="btn p-0 button_agregar_calidad rounded-circle text-white"
                  data-toggle="modal"
                  data-target="#exampleModal"
                >
                  <span>
                    <i class="fas fa-plus"></i>
                  </span>
                </button>
                <modal></modal>
              </div>
            </div>
            <div class="row justify-content-end">
              <div class>
                <div class="matris_liberacion text-center p-1">Proceso de liberacion</div>
              </div>
              <div class="col-md-4">
                <div class="matris_produccion text-center p-1">Durante produccion</div>
              </div>
            </div>
            <div class="row justify-content-end mt-2">
              <div class>
                <div class="row mx-3">
                  <div class="col-auto">Operador</div>
                  <div class="col-auto">Calidad</div>
                </div>
              </div>
              <div class="col-md-4">
                <div class="row mx-3">
                  <div class="col-auto">Operador</div>
                  <div class="col-auto">Calidad</div>
                </div>
              </div>
            </div>
            <!-- dragable matris -->
            <draggable :list="Preguntas" handle=".handle">
              <div class="row" v-for="(pregunta, idx) in Preguntas" :key="pregunta.id">
                <div class="col-lg-4">
                  <div class="row">
                    <div class="col-auto py-2">
                      <el-switch
                        v-model="pregunta.activado"
                        active-color="pregunta.activado"
                        inactive-color="pregunta.desactivado"
                      ></el-switch>
                    </div>
                    <div class="col-auto py-2">
                      <div class="drag_and_drop rounded-circle text-center text-white">
                        <span style="font-size: 15px;" class="handle">
                          <i class="fas fa-bars"></i>
                        </span>
                      </div>
                    </div>
                    <div class="col-md-4">
                      <div class="row texto_pregunta p-1">
                        <div class="col-md-11"> {{ pregunta.pregunta }}</div>
                        <div class="col-md-1">
                          <el-tooltip placement="right">
                            <button class="btn rounded-circle p-0 button_edit_calidad text-white">
                              <span style="font-size:15px;" class="p-1">
                                <i class="fas fa-ellipsis-v"></i>
                              </span>
                            </button>
                            <div class="d-table" slot="content">
                              <button class="d-table btn p-0 text-white">Editar</button>
                              <button class="d-table btn p-0 text-white" @click="EliminarPreguntas(idx)">Eliminar</button>
                            </div>
                          </el-tooltip>
                        </div>
                      </div>
                      <div class="Mostrar_Respuesta">{{ pregunta.respuesta }}</div>
                    </div>
                  </div>
                </div>
                <div class="col-lg-4 mx-auto pt-2">
                  <div class="row">
                    <div class="col-auto">
                      <el-checkbox
                        v-model="pregunta.liberacion_oper_checkbox"
                        size="medium"
                        class="liberacion_oper_checkbox"
                      ></el-checkbox>
                    </div>
                    <div class="col-auto">
                      <el-checkbox
                        v-model="pregunta.liberacion_calidad_checkbox"
                        size="medium"
                        class="liberacion_calidad_checkbox"
                      ></el-checkbox>
                    </div>
                    <div class="col-auto">
                      <el-checkbox
                        v-model="pregunta.produccion_oper_checkbox"
                        size="medium"
                        class="produccion_oper_checkbox"
                      ></el-checkbox>
                    </div>
                    <div class="col-auto">
                      <el-checkbox
                        v-model="pregunta.produccion_calidad_checkbox"
                        size="medium"
                        class="produccion_calidad_checkbox"
                      ></el-checkbox>
                    </div>
                  </div>
                </div>
              </div>
            </draggable>
            <!-- Dragable matris-->
          </div>
        </el-tab-pane>
        <el-tab-pane label="Motivos de calidad" name="second">
          <div class="motivos_devolucion">
            <!-- Hacerlo componenete -->
            <!-- Devolución -->
            <div class="row">
              <div
                class="col-md-3 text-center"
                style="color:#1F1B62;font-size:18px"
              >Tipos de motivos de calidad</div>
              <div class="col-md-7 h-75 mt-3 separador_devolucion">
                <!-- Este es el separador -->
              </div>
              <div class="col-md-2">
                <button
                  class="p-0 btn rounded-circle button_agregar_devolucion text-white"
                  slot="reference"
                  @click="VisibleCalidad = !VisibleCalidad"
                >
                  <span>
                    <i class="fas fa-plus"></i>
                  </span>
                </button>
                <!-- Popover Crear Motivos-->
                <el-popover
                  placement="bottom"
                  trigger="manual"
                  v-model="VisibleCalidad"
                  visible-arrow="true"
                  width="400"
                >
                  <div class="form_crear_devolucion">
                    <div class="row p-3 justify-content-center">Añadir motivo</div>
                    <div class="row mt-1 p-3">
                      <el-input placeholder="nombre" v-model="nombre_form_calidad"></el-input>
                    </div>
                    <div class="row mt-1 p-3">
                      <el-input
                        type="textarea"
                        placeholder="Descripción"
                        v-model="descripcion_form_calidad"
                      ></el-input>
                    </div>
                    <div class="row mt-1 p-3 justify-content-center">
                      <div class="contenedor_color_picker">
                        <el-color-picker v-model="colorCalidad" size="medium"></el-color-picker>
                      </div>
                    </div>
                    <div class="row justify-content-center">
                      <button class="btn btn-primary">Guardar</button>
                    </div>
                  </div>
                </el-popover>
                <!-- Popover Crear Motivos-->
              </div>
            </div>
            <!--  Devolución -->
            <!-- Devolución_comentario -->
            <div class="Motivo_devolucion_template my-2">
              <div class="row px-3">
                <div
                  class="color-circle-status rounded-circle p-1 mt-1"
                  style="width:16px;height:16px;"
                ></div>
                <div class="title_comentario_devolucion w-25 px-3">Evacuacion</div>
                <div class="ml-auto">
                  <el-tooltip placement="right">
                    <div slot="content" class="d-table">
                      <button class="d-table p-0 btn text-white">Editar</button>
                      <button class="d-table p-0 btn text-white">Eliminar</button>
                    </div>
                    <button class="btn p-0 rounded-circle button_comentario_devolucion text-white">
                      <i class="fas fa-ellipsis-v"></i>
                    </button>
                  </el-tooltip>
                </div>
              </div>
              <div class="row zona_comentario px-2 mx-3">
                Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quisquam pariatur fugiat iste corporis! Nemo
                ipsum eos eaque minus sit, animi quo! Consequatur illo eaque quibusdam. Unde porro incidunt dignissimos
                facere!
              </div>
            </div>
            <!-- Devolución comentario -->
            <!-- Hacerlo componenete -->
          </div>
        </el-tab-pane>
        <el-tab-pane label="Motivos de devolución" name="third">
          <div class="motivos_devolucion">
            <!-- Hacerlo componenete -->
            <!-- Devolución -->
            <div class="row">
              <div
                class="col-md-3 text-center"
                style="color:#1F1B62;font-size:18px;"
              >Tipos de motivos de devolución</div>
              <div class="col-md-7 h-75 mt-3 separador_devolucion">
                <!-- Este es el separador -->
              </div>
              <div class="col-md-2">
                <button
                  class="p-0 btn rounded-circle button_agregar_devolucion text-white"
                  slot="reference"
                  @click="VisibleDevolucion = !VisibleDevolucion"
                >
                  <span>
                    <i class="fas fa-plus"></i>
                  </span>
                </button>
                <!-- Popover Crear Motivos-->
                <el-popover
                  placement
                  trigger="manual"
                  v-model="VisibleDevolucion"
                  visible-arrow="true"
                  width="400"
                >
                  <div class="form_crear_devolucion">
                    <div class="row p-3 justify-content-center">Añadir motivo</div>
                    <div class="row mt-1 p-3">
                        <el-input placeholder="Nombre" v-model="nombre_form_devolucion"></el-input>
                    </div>
                    <div class="row mt-1 p-3">
                      <el-input
                        type="textarea"
                        placeholder="Descripción"
                        v-model="descripcion_form_devolucion"
                      ></el-input>
                    </div>
                    <div class="row mt-1 p-3 justify-content-center">
                      <div class="contenedor_color_picker">
                        <el-color-picker v-model="colorDevolucion" size="medium"></el-color-picker>
                      </div>
                    </div>
                    <div class="row justify-content-center">
                      <button class="btn btn-primary">Guardar</button>
                    </div>
                  </div>
                </el-popover>
                <!-- Popover Crear Motivos-->
              </div>
            </div>
            <!--  Devolución -->
            <!-- Devolución_comentario -->
            <div class="Motivo_devolucion_template my-2">
              <div class="row px-3">
                <div
                  class="color-circle-status rounded-circle p-1 mt-1"
                  style="width:16px;height: 16px;"
                ></div>
                <div class="title_comentario_devolucion w-25 px-3">Evacuacion</div>
                <div class="ml-auto">
                  <el-tooltip placement="right">
                    <button class="btn p-0 rounded-circle button_comentario_devolucion text-white">
                      <i class="fas fa-ellipsis-v"></i>
                    </button>
                    <div class="d-table" slot="content">
                      <button class="d-table p-0 btn text-white">Editar</button>
                      <button class="d-table p-0 btn text-white">Eliminar</button>
                    </div>
                  </el-tooltip>
                </div>
              </div>
              <div class="row zona_comentario px-2 mx-3">
                Lorem ipsum dolor sit, amet consectetur adipisicing elit. Quisquam pariatur fugiat iste corporis! Nemo
                ipsum eos eaque minus sit, animi quo! Consequatur illo eaque quibusdam. Unde porro incidunt dignissimos
                facere!
              </div>
            </div>
            <!-- Devolución comentario -->
            <!-- Hacerlo componenete -->
          </div>
        </el-tab-pane>
      </el-tabs>
    </div>
  </div>
</template>

<script>
import modal from "@/components/modal.vue";
import draggable from "vuedraggable";
export default {
  components: {
    modal,
    draggable
  },
  data() {
    return {
      colorCalidad: "#FD9644",
      nombre_form_calidad: "",
      colorDevolucion: "#FD9644",
      nombre_form_devolucion: "",
      descripcion_form_devolucion: "",
      visible: false,
      VisibleCalidad: false,
      VisibleDevolucion: false,
      descripcion_form_calidad: "",
      Preguntas : [
        {
          id: '0',
          pregunta : 'Esto es una pregunta de prueba',
          respuesta : 'Esto es una respuesta',
          liberacion_oper_checkbox : true,
          liberacion_calidad_checkbox: true,
          produccion_oper_checkbox: true,
          produccion_calidad_checkbox: true,
          desactivado: "#6C6B6B",
          activado: "#378EF6",
        },
        {
          id: '1',
          pregunta : 'Esto es una pregunta de prueba1',
          respuesta : 'Esto es una respuesta1',
          liberacion_oper_checkbox : true,
          liberacion_calidad_checkbox: true,
          produccion_oper_checkbox: true,
          produccion_calidad_checkbox: true
        },
        {
          id: '2',
          pregunta : 'Esto es una pregunta de prueba2',
          respuesta : 'Esto es una respuesta2',
          liberacion_oper_checkbox : true,
          liberacion_calidad_checkbox: true,
          produccion_oper_checkbox: true,
          produccion_calidad_checkbox: true
        },
        {
          id: '3',
          pregunta : 'Esto es una pregunta de prueba3',
          respuesta : 'Esto es una respuesta3',
          liberacion_oper_checkbox : true,
          liberacion_calidad_checkbox: true,
          produccion_oper_checkbox: true,
          produccion_calidad_checkbox: true
        }
      ]
    };
  },
  methods: {
    EliminarPreguntas(idx){
      this.Preguntas.splice(idx, 1);
    }
  }
};
</script>

<style lang="scss">

.el-popover{
    left: -174px;
    border-radius: 20px;
    border: solid;
    border-width: 1px;
    border-color: #32A3FD;

}

.Mostrar_Respuesta {
  color: #6c6b6b;
  width: 196px;
  min-height: 15px;
}

.matris_produccion {
  font-weight: bold;
  color: #32a3fd;
  width: 224px;
  height: 32px;
  border: solid;
  border-width: 1px;
  border-radius: 5px;
  border-color: #b7b7b7;
  background-color: #f3f3f3;
}

.matris_liberacion {
  font-weight: bold;
  color: #32a3fd;
  width: 224px;
  height: 32px;
  border: solid;
  border-width: 1px;
  border-radius: 5px;
  border-color: #b7b7b7;
  background-color: #f3f3f3;
}

.Motivo_devolucion_template {
  padding: 9px;
  border: solid 1px;
  border-color: #e3e1e1;
  width: 899px;
  height: 99px;
  border-radius: 5px;
}

.button_comentario_devolucion {
  width: 29px;
  height: 29px;
  background-color: #32a3fd;
  box-shadow: 0px 3px 6px #32a3fd99;
}

.color-circle-status {
  background-color: #fd9644;
}

.button_agregar_devolucion {
  background-color: #32a3fd;
  box-shadow: 0px 3px 9px #32a3fd99;
  height: 30px;
  width: 30px;
}

.separador_devolucion {
  border: solid;
  border-width: 1px;
  border-color: rgb(227, 225, 225);
}

.motivos_devolucion {
  height: 752px;
}

.produccion_calidad_checkbox {
  margin-left: 44px;
}

.produccion_oper_checkbox {
  margin-left: 94px;
}

.liberacion_calidad_checkbox {
  margin-left: 51px;
}

.liberacion_oper_checkbox {
  margin-left: 77px;
}

.texto_pregunta {
  border-radius: 5px;
  width: 472px;
  min-height: 49px;
  border: solid;
  border-color: #e3e1e1;
  border-width: 1px;
}

.button_edit_calidad {
  width: 24px;
  height: 24px;
  background-color: #32a3fd;
  box-shadow: #32a3fd99;
  opacity: 1;
  color: white;
}

.drag_and_drop {
  cursor: pointer;
  width: 25px;
  height: 25px;
  background-color: #32a3fd;
  box-shadow: 0px 3px 6px #006ec53f;
}

.button_agregar_calidad {
  background-color: #32a3fd;
  box-shadow: 0px 3px 6px #32a3fd99;
  width: 29px;
  height: 29px;
}

.separador_calidad_preguntas {
  border: solid;
  border-width: 2px;
  border-color: rgb(227, 225, 225);
}

.contenedor-calidad {
  /* width: 1281px; */
  height: 752px;
  background-color: #ffffff;
  box-shadow: 0px 3px 6px #00000029;
}

#header {
  /* //width: 1316px; */
  height: 50px;
  background-color: #ffffff;
  box-shadow: 0px 3px 6px #00000029;
}
</style>
