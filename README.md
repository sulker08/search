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


