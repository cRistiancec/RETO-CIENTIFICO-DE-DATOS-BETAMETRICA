RETO CIENTIFICO DE DATOS
================
Cristian Coronel Quezada
2023-10-27

\#————-Cargando librerías—————-#

``` r
#Ctrl + a , para seleccionar todo
#Ctrl + Alt + i , para abrir un nuevo chunk

#install.packages("dplyr") cuando no se tiene descargado aún la libreria

library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(openxlsx)
```

\#————-Cargar base de datos—————-#

``` r
datos <- read.xlsx("D:/RETO CIENTIFICO DE DATOS/DATA/empresas_HEBM18.xlsx", na.strings = T)
head(datos)
```

    ##   2019 2018 PR EXPEDIENTE
    ## 1   56 5027  1     715075
    ## 2  134  149  2      44552
    ## 3  135  158  3     176111
    ## 4  143  168  4     170865
    ## 5  360  297  5      62692
    ## 6  379  442  6      19757
    ##                                                                              NOMBRE
    ## 1                                    PTIE- PHOENIX TOWER INTERNATIONAL ECUADOR S.A.
    ## 2                                                                          CNO S.A.
    ## 3                                          FARIBALL HOLDING CORP. C.A. FARIBALLCORP
    ## 4                                                                      VICGRUP S.A.
    ## 5 CHINA HIDROELECTRICIDAD INGENIERIA CONSULTORIO GRUPO CO. (HYDROCHINA CORPORATION)
    ## 6                                          VIVIENDAS MASIVAS ECUATORIANAS VIMARE SA
    ##          TIPO.COMPAÑIA
    ## 1              ANÓNIMA
    ## 2 SUCURSAL  EXTRANJERA
    ## 3              ANÓNIMA
    ## 4              ANÓNIMA
    ## 5 SUCURSAL  EXTRANJERA
    ## 6              ANÓNIMA
    ##                                                                                                                                                                                                                                                                                                                                                                                                        ACTIVIDAD.ECONÓMICA
    ## 1                                                                                                                                 F4321.01 - INSTALACIÓN DE ACCESORIOS ELÉCTRICOS, LÍNEAS DE TELECOMUNICACIONES, REDES INFORMÁTICAS Y LÍNEAS DE TELEVISIÓN POR CABLE, INCLUIDAS LÍNEAS DE FIBRA ÓPTICA, ANTENAS PARABÓLICAS. INCLUYE CONEXIÓN DE APARATOS ELÉCTRICOS, EQUIPO DOMÉSTICO Y SISTEMAS DE CALEFACCIÓN RADIANTE.
    ## 2                                                                                                                                                                                                                                                                                                                       F4210.11 - CONSTRUCCIÓN DE CARRETERAS, CALLES, CARRETERAS, Y OTRAS VÍAS PARA VEHÍCULOS O PEATONES.
    ## 3 K6420.00 - ACTIVIDADES DE SOCIEDADES DE CARTERA, ES DECIR, UNIDADES TENEDORAS DE ACTIVOS DE UN GRUPO DE EMPRESAS FILIALES (CON PARTICIPACIÓN DE CONTROL EN SU CAPITAL SOCIAL) Y CUYA ACTIVIDAD PRINCIPAL CONSISTE EN LA PROPIEDAD DEL GRUPO. LAS SOCIEDADES DE CARTERA CLASIFICADAS EN ESTA CLASE NO SUMINISTRAN NINGÚN OTRO SERVICIO A LAS EMPRESAS PARTICIPADAS, ES DECIR, NO ADMINISTRAN NI GESTIONAN OTRAS UNIDADES.
    ## 4 K6420.00 - ACTIVIDADES DE SOCIEDADES DE CARTERA, ES DECIR, UNIDADES TENEDORAS DE ACTIVOS DE UN GRUPO DE EMPRESAS FILIALES (CON PARTICIPACIÓN DE CONTROL EN SU CAPITAL SOCIAL) Y CUYA ACTIVIDAD PRINCIPAL CONSISTE EN LA PROPIEDAD DEL GRUPO. LAS SOCIEDADES DE CARTERA CLASIFICADAS EN ESTA CLASE NO SUMINISTRAN NINGÚN OTRO SERVICIO A LAS EMPRESAS PARTICIPADAS, ES DECIR, NO ADMINISTRAN NI GESTIONAN OTRAS UNIDADES.
    ## 5                                                                                                                                                                                   D3510.01 - ACTIVIDADES DE OPERACIÓN DE INSTALACIONES DE GENERACIÓN DE ENERGÍA ELÉCTRICA, POR DIVERSOS MEDIOS: TÉRMICA (TURBINA DE GAS O DIESEL), NUCLEAR, HIDROELÉCTRICA, SOLAR, MAREAL Y DE OTROS TIPOS INCLUSO DE ENERGÍA RENOVABLE.
    ## 6                           L6810.01 - COMPRA - VENTA, ALQUILER Y EXPLOTACIÓN DE BIENES INMUEBLES PROPIOS O ARRENDADOS, COMO: EDIFICIOS DE APARTAMENTOS Y VIVIENDAS; EDIFICIOS NO RESIDENCIALES, INCLUSO SALAS DE EXPOSICIONES; INSTALACIONES PARA ALMACENAJE, CENTROS COMERCIALES Y TERRENOS; INCLUYE EL ALQUILER DE CASAS Y APARTAMENTOS AMUEBLADOS O SIN AMUEBLAR POR PERÍODOS LARGOS, EN GENERAL POR MESES O POR AÑOS.
    ##   REGION                                          PROVINCIA
    ## 1 SIERRA PICHINCHA                                         
    ## 2  COSTA GUAYAS                                            
    ## 3  COSTA GUAYAS                                            
    ## 4  COSTA GUAYAS                                            
    ## 5 SIERRA PICHINCHA                                         
    ## 6  COSTA GUAYAS                                            
    ##                                               CIUDAD  TAMAÑO     SECTOR
    ## 1 QUITO                                              PEQUEÑA SOCIETARIO
    ## 2 GUAYAQUIL                                          PEQUEÑA SOCIETARIO
    ## 3 SAMBORONDÓN                                        PEQUEÑA SOCIETARIO
    ## 4 GUAYAQUIL                                          PEQUEÑA SOCIETARIO
    ## 5 QUITO                                              PEQUEÑA SOCIETARIO
    ## 6 GUAYAQUIL                                          PEQUEÑA SOCIETARIO
    ##   CANT..EMPLEADOS    ACTIVO PATRIMONIO INGRESOS.POR.VENTA  UTILIDAD  INGRESOS
    ## 1              11 243754719  6801812.0          453431.30      0.00 453431.30
    ## 2               2 112423770 20857949.8               0.00      0.00      0.00
    ## 3               4 111463482   792412.8               0.00 994057.78      0.00
    ## 4               2 107772498 64080222.1           55567.84      0.00  55567.84
    ## 5              77  46186116 -9926289.9               0.00      0.00      0.00
    ## 6               4  44219420 36538029.4          521976.23   1585.05 521976.23

``` r
str(datos)
```

    ## 'data.frame':    19456 obs. of  18 variables:
    ##  $ 2019               : chr  "56" "134" "135" "143" ...
    ##  $ 2018               : chr  "5027" "149" "158" "168" ...
    ##  $ PR                 : chr  "1" "2" "3" "4" ...
    ##  $ EXPEDIENTE         : chr  "715075" "44552" "176111" "170865" ...
    ##  $ NOMBRE             : chr  "PTIE- PHOENIX TOWER INTERNATIONAL ECUADOR S.A." "CNO S.A." "FARIBALL HOLDING CORP. C.A. FARIBALLCORP" "VICGRUP S.A." ...
    ##  $ TIPO.COMPAÑIA      : chr  "ANÓNIMA" "SUCURSAL  EXTRANJERA" "ANÓNIMA" "ANÓNIMA" ...
    ##  $ ACTIVIDAD.ECONÓMICA: chr  "F4321.01 - INSTALACIÓN DE ACCESORIOS ELÉCTRICOS, LÍNEAS DE TELECOMUNICACIONES, REDES INFORMÁTICAS Y LÍNEAS DE T"| __truncated__ "F4210.11 - CONSTRUCCIÓN DE CARRETERAS, CALLES, CARRETERAS, Y OTRAS VÍAS PARA VEHÍCULOS O PEATONES." "K6420.00 - ACTIVIDADES DE SOCIEDADES DE CARTERA, ES DECIR, UNIDADES TENEDORAS DE ACTIVOS DE UN GRUPO DE EMPRESA"| __truncated__ "K6420.00 - ACTIVIDADES DE SOCIEDADES DE CARTERA, ES DECIR, UNIDADES TENEDORAS DE ACTIVOS DE UN GRUPO DE EMPRESA"| __truncated__ ...
    ##  $ REGION             : chr  "SIERRA" "COSTA" "COSTA" "COSTA" ...
    ##  $ PROVINCIA          : chr  "PICHINCHA                                         " "GUAYAS                                            " "GUAYAS                                            " "GUAYAS                                            " ...
    ##  $ CIUDAD             : chr  "QUITO                                             " "GUAYAQUIL                                         " "SAMBORONDÓN                                       " "GUAYAQUIL                                         " ...
    ##  $ TAMAÑO             : chr  "PEQUEÑA" "PEQUEÑA" "PEQUEÑA" "PEQUEÑA" ...
    ##  $ SECTOR             : chr  "SOCIETARIO" "SOCIETARIO" "SOCIETARIO" "SOCIETARIO" ...
    ##  $ CANT..EMPLEADOS    : num  11 2 4 2 77 4 5 4 5 0 ...
    ##  $ ACTIVO             : num  2.44e+08 1.12e+08 1.11e+08 1.08e+08 4.62e+07 ...
    ##  $ PATRIMONIO         : num  6801812 20857950 792413 64080222 -9926290 ...
    ##  $ INGRESOS.POR.VENTA : num  453431 0 0 55568 0 ...
    ##  $ UTILIDAD           : num  0 0 994058 0 0 ...
    ##  $ INGRESOS           : num  453431 0 0 55568 0 ...

``` r
names(datos)
```

    ##  [1] "2019"                "2018"                "PR"                 
    ##  [4] "EXPEDIENTE"          "NOMBRE"              "TIPO.COMPAÑIA"      
    ##  [7] "ACTIVIDAD.ECONÓMICA" "REGION"              "PROVINCIA"          
    ## [10] "CIUDAD"              "TAMAÑO"              "SECTOR"             
    ## [13] "CANT..EMPLEADOS"     "ACTIVO"              "PATRIMONIO"         
    ## [16] "INGRESOS.POR.VENTA"  "UTILIDAD"            "INGRESOS"

\#————–Manejo de bases de datos—————-#

``` r
#pipe  %>% 
#select
#filter

#shortcut %>%   ctrl+shift+m
#asigno <-  alt+ - 

datos <- datos %>% filter(complete.cases(.))

nuevadata <- datos %>% 
  select(NOMBRE,REGION,PROVINCIA,CIUDAD,INGRESOS,CANT..EMPLEADOS,UTILIDAD) %>% 
  filter(INGRESOS <= 100000 & INGRESOS > 10000)


#CAMBIANDO DE ESCALA

nuevadata$INGRESOS <- nuevadata$INGRESOS /1000
nuevadata$INGRESOS <- nuevadata$INGRESOS /1000

#INSPECCIONANDO BASE DE DATOS

summary(nuevadata)
```

    ##     NOMBRE             REGION           PROVINCIA            CIUDAD         
    ##  Length:339         Length:339         Length:339         Length:339        
    ##  Class :character   Class :character   Class :character   Class :character  
    ##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
    ##                                                                             
    ##                                                                             
    ##                                                                             
    ##     INGRESOS       CANT..EMPLEADOS      UTILIDAD     
    ##  Min.   :0.01077   Min.   :   0.00   Min.   :     0  
    ##  1st Qu.:0.04145   1st Qu.:   4.00   1st Qu.: 22201  
    ##  Median :0.07242   Median :   4.00   Median : 54695  
    ##  Mean   :0.06584   Mean   :  32.71   Mean   :113792  
    ##  3rd Qu.:0.09129   3rd Qu.:   7.00   3rd Qu.:138878  
    ##  Max.   :0.10000   Max.   :8866.00   Max.   :897481

\#———-Funciones super poderosas de dplyr———–#

``` r
#group_by
#summarise
#arrange

nuevadata2 <- nuevadata %>% 
  group_by(REGION) %>% 
  summarise(PROM_INGRESOS=mean(INGRESOS)) %>% 
  arrange(-PROM_INGRESOS)

nuevadata2
```

    ## # A tibble: 4 × 2
    ##   REGION    PROM_INGRESOS
    ##   <chr>             <dbl>
    ## 1 SIERRA           0.0687
    ## 2 GALAPAGOS        0.0677
    ## 3 COSTA            0.0633
    ## 4 ORIENTE          0.0541

``` r
nuevadata2 <- nuevadata %>% 
  group_by(REGION,CIUDAD) %>% 
  summarise(PROM_INGRESOS=mean(INGRESOS),
            MAX_INGRESOS=max(INGRESOS)) %>% 
  arrange(-PROM_INGRESOS)
```

    ## `summarise()` has grouped output by 'REGION'. You can override using the
    ## `.groups` argument.

``` r
nuevadata2
```

    ## # A tibble: 40 × 4
    ## # Groups:   REGION [4]
    ##    REGION CIUDAD                                      PROM_INGRESOS MAX_INGRESOS
    ##    <chr>  <chr>                                               <dbl>        <dbl>
    ##  1 SIERRA "SANTA ISABEL                             …        0.0976       0.0976
    ##  2 SIERRA "SANTA ROSA DE CUSUBAMBA                  …        0.0951       0.0951
    ##  3 SIERRA "SARAGURO                                 …        0.0949       0.0949
    ##  4 COSTA  "SALINAS                                  …        0.0939       0.0939
    ##  5 COSTA  "MANTA                                    …        0.0932       0.0932
    ##  6 COSTA  "NARANJAL                                 …        0.0902       0.0902
    ##  7 SIERRA "SANGOLQUÍ                                …        0.0898       0.0913
    ##  8 SIERRA "MACHACHI                                 …        0.0891       0.0891
    ##  9 COSTA  "ATACAMES                                 …        0.0891       0.0891
    ## 10 COSTA  "DAULE                                    …        0.0887       0.099 
    ## # ℹ 30 more rows
