# search<style>
    .card-space {
        padding: 2%;
    }

    .imagenportada {
        min-height: 35vh;
        padding: 2%;
        background-position: center;
        background-size: cover;
        background-repeat: no-repeat;
        transition: all .5s;
    }

    .dropdown-toggle::after {
        content: none;
    }

    .dropdown-menu {
        min-width: 0 !important;
    }
</style>
<div class="container">
    <?php if (isset($error)) : ?>
        <div class="row">
            <div class="alert alert-warning alert-dismissible fade show" role="alert">
                <strong>Información: </strong> <?php echo $error; ?>
                <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
            </div>
        </div>
    <?php endif; ?>
    <?php visualinmu_load_template("inmuebles/search-form.php", get_defined_vars()); ?>
    <div class="row">
        <div class="col<?php echo visualinmu_is_sidebar_active("lateral_pagina_propiedades_visual_inmueble") ? "-md-9" : "-md-12"; ?>">
            <?php if (isset($inmuebles)) : ?>
                <?php $nombreShowTab = visualinmu_config_search_tab_show();?>
                <ul class="nav nav-tabs" id="tabSearch" role="tablist">
                    <li class="nav-item" role="presentation">
                        <button class="nav-link <?php echo 'lista' == $nombreShowTab ? 'active' : ''?>" id="lista-tab" data-bs-toggle="tab" data-bs-target="#lista"
                                type="button"
                                role="tab" aria-controls="home" aria-selected="true"><i class="icon icon-uniE911"></i>
                            Lista
                        </button>
                    </li>
                    <li class="nav-item" role="presentation">
                        <button class="nav-link <?php echo 'mapa' == $nombreShowTab ? 'active' : ''?>" id="mapa-tab" data-bs-toggle="tab" data-bs-target="#mapa" type="button"
                                role="tab" aria-controls="profile" aria-selected="false"><i
                                    class="icon icon-uniE912"></i>
                            Mapa
                        </button>
                    </li>
                </ul>
                <div class="tab-content" id="myTabContent">
                    <div class="tab-pane fade <?php echo 'lista' == $nombreShowTab ? 'active show' : ''?>" id="lista" role="tabpanel" aria-labelledby="home-tab">
                        <div class="row">
                            <?php if (count($inmuebles) > 0) : ?>
                                <?php foreach ($inmuebles as $cont => $inmueble) : ?>
                                    <div class="col-xs-12 col-md-4 card-space">
                                        <div class="card" style="width: 100%; padding: 2%;">
                                            <a href="<?php echo visualinmu_route_detalleInmueble($inmueble->slug()); ?>"
                                               target="_blank">
                                                <div class="imagenportada"
                                                     style="background-image: url(<?php echo $inmueble->fotoPortada(); ?>);">
                                                    <?php if ($inmueble->gestion()->esArriendoVenta()) : ?>
                                                        <span class="badge rounded-pill bg-primary"><i
                                                                    class="icon icon-uniE9C2"></i> VENTA</span>
                                                        <span class="badge rounded-pill bg-light text-dark"><i
                                                                    class="icon icon-uniE9C2"></i> ARRIENDO</span>
                                                    <?php elseif ($inmueble->gestion()->esAriendo()) : ?>
                                                        <span class="badge rounded-pill bg-light text-dark"><i
                                                                    class="icon icon-uniE9C2"></i> ARRIENDO</span>
                                                    <?php else : ?>
                                                        <span class="badge rounded-pill bg-primary"><i
                                                                    class="icon icon-uniE9C2"></i> VENTA</span>
                                                    <?php endif; ?>
                                                </div>
                                            </a>
                                            <div class="card-body">
                                                <p>
                                                    <a href="<?php echo visualinmu_route_detalleInmueble($inmueble->slug()); ?>" ><h5
                                                        class="card-title"><?php echo $inmueble->nombre(); ?></h5></a>
                                                <p><i class="icon icon-uniE978"></i>
                                                    Código: <?php echo $inmueble->codigo(); ?></p>
                                                <a href="<?php echo visualinmu_route_detalleInmueble($inmueble->slug()); ?>" class="vi-link-ubicacion" >
                                                    <i class="icon icon-uniE91C"></i> <?php echo $inmueble->ciudad()->nombre(); ?>
                                                    - <?php echo $inmueble->departamento()->nombre(); ?></a></p>
                                                <p class="card-text">
                                                    <?php if ($inmueble->gestion()->esArriendoVenta()) : ?>
													<p class="precios"><strong>V. venta</strong>
														$<?php echo $inmueble->valorVenta(true); ?> <sub>COP</sub></p>
													<p class="precios"><strong>V. arriendo</strong>
														$<?php echo $inmueble->valorCanon(true); ?> <sub>COP</sub></p>
													<?php elseif ($inmueble->gestion()->esAriendo()) : ?>
														<p class="precios"><strong>V. arriendo</strong>
															$<?php echo $inmueble->valorCanon(true); ?> <sub>COP</sub></p>
													<?php else : ?>
														<p class="precios"><strong>V. venta</strong>
															$<?php echo $inmueble->valorVenta(true); ?> <sub>COP</sub></p>
													<?php endif; ?>
                                                </p>
                                                <hr>
                                                <div class="row d-flex justify-content-center text-center">
                                                    <div class="col">
                                                        <p>
                                                            <i class="icon icon-uniE938"></i> <?php echo $inmueble->nAlcobas(); ?>
                                                            Alcoba(s)
                                                        </p>
                                                    </div>
                                                    <div class="col">
                                                        <p>
                                                            <i class="icon icon-uniE93E"></i> <?php echo $inmueble->nBaños(); ?>
                                                            Baño(s)
                                                        </p>
                                                    </div>
                                                    <div class="col">
                                                        <p>
                                                            <i class="icon icon-uniE9CC"></i> <?php echo $inmueble->nGarajes(); ?>
                                                            Garaje(s)
                                                        </p>
                                                    </div>
                                                    <div class="col vi-compartir-inmuebles">
                                                        <div class="dropdown">
                                                            <a class="dropdown-toggle" href="#" role="button"
                                                               id="dropdownMenuLink" data-bs-toggle="dropdown"
                                                               aria-expanded="false"><i
                                                                        class="fas fa-share-alt  vi-icono-compartir"></i></a>
                                                            <ul class="dropdown-menu"
                                                                aria-labelledby="dropdownMenuLink">
                                                                <li>
                                                                    <a class="dropdown-item"
                                                                       href="<?php echo visualinmu_redsocial_url(["nombre" => "facebook"], visualinmu_route_detalleInmueble($inmueble->slug())); ?>"
                                                                       target="_blank"><i
                                                                                class="fab fa-facebook-f"></i></a>
                                                                </li>
                                                                <li><a class="dropdown-item"
                                                                       href="<?php echo visualinmu_redsocial_url(["nombre" => "linkedin"], visualinmu_route_detalleInmueble($inmueble->slug())); ?>"
                                                                       target="_blank"><i
                                                                                class="fab fa-linkedin-in"></i></a>
                                                                </li>
                                                                <li><a class="dropdown-item"
                                                                       href="<?php echo visualinmu_redsocial_url(["nombre" => "twitter"], visualinmu_route_detalleInmueble($inmueble->slug())); ?>"
                                                                       target="_blank"><i
                                                                                class="fab fa-twitter"></i></a>
                                                                </li>
                                                                <li><a class="dropdown-item"
                                                                       href="<?php echo visualinmu_redsocial_url(["nombre" => "whatsapp"], visualinmu_route_detalleInmueble($inmueble->slug())); ?>"
                                                                       target="_blank"><i
                                                                                class="fab fa-whatsapp"></i></a>
                                                                </li>
                                                            </ul>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                <?php endforeach; ?>
                            <?php else : ?>
                                <label> Sin Resultados </label>
                            <?php endif; ?>
                            <?php if (isset($paginador)) : visualinmu_load_template("inmuebles/paginator-form.php", ["paginador" => $paginador]); endif; ?>
                        </div>
                    </div>
                    <div class="tab-pane fade <?php echo 'mapa' == $nombreShowTab ? 'active show' : ''?> " id="mapa" role="tabpanel" aria-labelledby="profile-tab">
                        <?php if('mapa' == $nombreShowTab){?>
                            <visualinmueble-map></visualinmueble-map>
                        <?php }; ?>
                    </div>
                </div>
                <script type="text/javascript">
                    window.inmuebles =  <?php echo json_encode($inmuebles, JSON_PRETTY_PRINT);?>;

                </script>
            <?php endif; ?>
        </div>
        <?php if (visualinmu_is_sidebar_active("lateral_pagina_propiedades_visual_inmueble")): ?>
            <div class="col-md-3">
                <?php dynamic_sidebar('lateral_pagina_propiedades_visual_inmueble'); ?>
            </div>
        <?php endif; ?>
    </div>
</div>


<?php if (isset($form)): ?>
    <form class="row  visualinmueble-formulario-widget-busqueda" id="<?php echo $form["id"]; ?>"
          action="<?php echo $form["action"]; ?>" method="<?php echo $form["method"]; ?>"
          x-data="VISUALINMU_SEARCH_FORM">
        <?php if (isset($form["filters"]["sede"]["old"])) { ?>
            <input class="form-control" type="hidden" name="<?php echo $form["filters"]["sede"]["inputName"]; ?>"
                   value="<?php echo !empty($form["filters"]["sede"]["old"]) ? $form["filters"]["sede"]["old"] : ""; ?>"/>
        <?php } ?>

        <div class="col-md-2 visua_inmueble_codigo">
            <label for="floatingInputGrid"><?php echo $form["filters"]["codigo"]["label"]; ?></label>
            <input type="text" class="form-control" id="floatingInputGrid"
                   name="<?php echo $form["filters"]["codigo"]["inputName"]; ?>"
                   value="<?php echo !empty($form["filters"]["codigo"]["old"]) ? $form["filters"]["codigo"]["old"] : ""; ?>">
        </div>
        <div class="col-md-2 visua_inmueble_tipo_inmueble">
            <label for="floatingInputGrid"><?php echo $form["filters"]["tipoInmueble"]["label"]; ?></label>
            <select class="form-control" id="<?php echo $form["filters"]["tipoInmueble"]["id"] ?>"
                    name="<?php echo $form["filters"]["tipoInmueble"]["inputName"]; ?>">
                <option value="" <?php echo empty($form["filters"]["tipoInmueble"]["old"]) ? "selected" : "" ?>
                ><?php echo $form["filters"]["tipoInmueble"]["label"]; ?></option>
                <template x-for="tipoInmueble in tiposInmueble">
                    <option x-model="tipoInmueble.codigo" x-text="tipoInmueble.nombre"></option>
                </template>
                <?php foreach ($form["filters"]["tipoInmueble"]["options"] as $tipoInmueble): ?>
                    <option value="<?php echo $tipoInmueble->codigo(); ?>"
                        <?php echo $tipoInmueble->codigo() == $form["filters"]["tipoInmueble"]["old"] ? "selected" : "" ?>
                    ><?php echo $tipoInmueble->nombre(); ?></option>
                <?php endforeach; ?>
            </select>
        </div>
        <div class="col-md-2 visua_inmueble_tipo_gestion">
            <label for="floatingInputGrid"><?php echo $form["filters"]["tipoGestion"]["label"]; ?></label>
            <select class="form-control" id="<?php echo $form["filters"]["tipoGestion"]["id"] ?>"
                    name="<?php echo $form["filters"]["tipoGestion"]["inputName"]; ?>">
                <option value="" <?php echo empty($form["filters"]["tipoGestion"]["old"]) ? "selected" : "" ?>
                ><?php echo $form["filters"]["tipoGestion"]["label"]; ?></option>
                <template x-for="tipoGestion in tiposGestion">
                    <option x-model="tipoGestion.codigo" x-text="tipoGestion.nombre"></option>
                </template>
                <?php foreach ($form["filters"]["tipoGestion"]["options"] as $tipoGestion): ?>
                    <option value="<?php echo $tipoGestion->codigo(); ?>"
                        <?php echo $tipoGestion->codigo() == $form["filters"]["tipoGestion"]["old"] ? "selected" : "" ?>
                    ><?php echo $tipoGestion->nombre(); ?></option>
                <?php endforeach; ?>
            </select>
        </div>
        <div class="col-md-2 visua_inmueble_departamentos">
            <label for="floatingInputGrid"><?php echo $form["filters"]["departamentos"]["label"]; ?></label>
            <select class="form-control" name="<?php echo $form["filters"]["departamentos"]["inputName"] ?>"
                    id="<?php echo $form["filters"]["departamentos"]["id"]; ?>"
                    x-model="tipoDepartamentoSelect"
                    x-on:change="cambioDepartamento($event)">
                <option value="" <?php echo empty($form["filters"]["departamentos"]["old"]) ? "selected" : "" ?>
                ><?php echo $form["filters"]["departamentos"]["label"]; ?></option>
                <template x-for="departamento in departamentos">
                    <option x-model="departamento.codigo" x-text="departamento.nombre"></option>
                </template>
                <?php
                /**
                 * @var $departamento \DDD\Modelos\Departamento
                 */
                foreach ($form["filters"]["departamentos"]["options"] as $departamento): ?>
                    <option value="<?php echo $departamento->codigo(); ?>"
                        <?php echo $departamento->codigo() == $form["filters"]["departamentos"]["old"] ? "selected" : "" ?>
                    ><?php echo $departamento->nombre(); ?></option>
                <?php endforeach; ?>
            </select>
        </div>
        <div class="col-md-2 visua_inmueble_ciudades">
            <label for="floatingInputGrid"><?php echo $form["filters"]["ciudades"]["label"]; ?></label>
            <select class="form-control" name="<?php echo $form["filters"]["ciudades"]["inputName"] ?>"
                    id="<?php echo $form["filters"]["ciudades"]["id"]; ?>" x-model="ciudadSelected"
                    x-on:change="cambioCiudad($event)">
                <option value="" <?php echo empty($form["filters"]["ciudades"]["old"]) ? "selected" : "" ?>
                ><?php echo $form["filters"]["ciudades"]["label"]; ?></option>
                <template x-for="ciudad in ciudades">
                    <option :selected="ciudad.codigo == ciudadSelected" :key="ciudad.codigo" :value="ciudad.codigo"
                            x-text="ciudad.nombre"></option>
                </template>
            </select>
        </div>
        <div class="col-md-2 visua_inmueble_barrios">
            <label for="floatingInputGrid"><?php echo $form["filters"]["barrios"]["label"]; ?></label>
            <select class="form-control" name="<?php echo $form["filters"]["barrios"]["inputName"] ?>"
                    id="<?php echo $form["filters"]["barrios"]["id"]; ?>" x-model="barrioSelected"
                    x-on:change="cambioBarrio($event)">
                <option value="" <?php echo empty($form["filters"]["barrios"]["old"]) ? "selected" : "" ?>
                ><?php echo $form["filters"]["barrios"]["label"]; ?></option>
                <template x-for="barrio in barrios">
                    <option :selected="barrio.codigo==barrioSelected" :key="barrio.codigo" :value="barrio.codigo"
                            x-text="barrio.nombre"></option>
                </template>
            </select>
        </div>
        <div class="col-md-2 visua_inmueble_precio_minimo">
            <label for="floatingInputGrid"><?php echo $form["filters"]["precioMin"]["label"]; ?></label>
            <input type="text" class="form-control <?php echo $form["filters"]["precioMax"]["class"]; ?>"
                   id="floatingInputGrid"
                   name="<?php echo $form["filters"]["precioMin"]["inputName"]; ?>"
                   value="<?php echo !empty($form["filters"]["precioMin"]["old"]) ? $form["filters"]["precioMin"]["old"] : ""; ?>">
        </div>
        <div class="col-md-2 visua_inmueble_precio_maximo">
            <label for="floatingInputGrid"><?php echo $form["filters"]["precioMax"]["label"]; ?></label>
            <input type="text" class="form-control <?php echo $form["filters"]["precioMax"]["class"]; ?>"
                   id="floatingInputGrid"
                   name="<?php echo $form["filters"]["precioMax"]["inputName"]; ?>"
                   value="<?php echo !empty($form["filters"]["precioMax"]["old"]) ? $form["filters"]["precioMax"]["old"] : ""; ?>">

        </div>
        <div class="col-md-2 visua_inmueble_area_maximo">
            <label for="floatingInputGrid"><?php echo $form["filters"]["areaMax"]["label"]; ?></label>
            <input type="number" class="form-control <?php echo $form["filters"]["precioMax"]["class"]; ?>"
                   id="floatingInputGrid"
                   name="<?php echo $form["filters"]["areaMax"]["inputName"]; ?>"
                   value="<?php echo !empty($form["filters"]["areaMax"]["old"]) ? $form["filters"]["areaMax"]["old"] : ""; ?>">
        </div>
        <div class="col-md-2  visua_inmueble_area_minima">
            <label for="floatingInputGrid"><?php echo $form["filters"]["areaMin"]["label"]; ?></label>
            <input type="number" class="form-control <?php echo $form["filters"]["precioMax"]["class"]; ?>"
                   id="floatingInputGrid"
                   name="<?php echo $form["filters"]["areaMin"]["inputName"]; ?>"
                   value="<?php echo !empty($form["filters"]["areaMin"]["old"]) ? $form["filters"]["areaMin"]["old"] : ""; ?>">
        </div>
        <div class="col-md-2 visua_inmueble_banos">
            <label for="floatingInputGrid"><?php echo $form["filters"]["baños"]["label"]; ?></label>
            <input type="number" class="form-control <?php echo $form["filters"]["precioMax"]["class"]; ?>"
                   id="floatingInputGrid"
                   name="<?php echo $form["filters"]["baños"]["inputName"]; ?>"
                   value="<?php echo !empty($form["filters"]["baños"]["old"]) ? $form["filters"]["baños"]["old"] : ""; ?>">

        </div>
        <div class="col-md-2 visua_inmueble_alcobas">
            <label for="floatingInputGrid"><?php echo $form["filters"]["alcobas"]["label"]; ?></label>
            <input type="number" class="form-control <?php echo $form["filters"]["precioMax"]["class"]; ?>"
                   id="floatingInputGrid"
                   name="<?php echo $form["filters"]["alcobas"]["inputName"]; ?>"
                   value="<?php echo !empty($form["filters"]["alcobas"]["old"]) ? $form["filters"]["alcobas"]["old"] : ""; ?>">

        </div>
        <div class="col-md-2 visua_inmueble_garajes">
            <label for="floatingInputGrid"><?php echo $form["filters"]["garajes"]["label"]; ?></label>
            <input type="number" class="form-control <?php echo $form["filters"]["precioMax"]["class"]; ?>"
                   id="floatingInputGrid"
                   name="<?php echo $form["filters"]["garajes"]["inputName"]; ?>"
                   value="<?php echo !empty($form["filters"]["garajes"]["old"]) ? $form["filters"]["garajes"]["old"] : ""; ?>">
        </div>
        <div class="col-md-2 boton-buscar">
            <input type="submit" class="btn btn-primary btn-bus" value="Buscar">
        </div>
        <div class="col-md-2  boton-limpiar">
            <a href="<?php echo $form["clear"]; ?>" class="btn btn-primary btn-lim">Limpiar</a>
        </div>
    </form>
<?php endif; ?>
<br><br>
