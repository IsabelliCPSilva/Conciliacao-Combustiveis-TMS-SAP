🔄 Conciliación de Combustibles TMS × SAP

Proyecto real desarrollado por Isabelli Cristina Pereira da Silva
Analista de Costes · Expresso 3300 Transportes LTDA · 2025–2026


📌 Contexto del Problema
La empresa operaba con dos sistemas independientes que registraban los mismos abastecimientos de combustible de formas completamente diferentes:
SistemaFunciónProblemaTMS (Sistema de Gestión de Transporte)Registro operativo realizado por el conductor en el momento del abastecimientoNombre del punto de suministro informal o abreviadoSAP (Sistema Financiero — Razón Contable)Registro financiero generado al emitir la facturaNombre del punto de suministro como razón social completa
El resultado: ninguno de los dos sistemas podía cruzar los datos del otro automáticamente. La empresa no sabía con precisión si lo que se estaba pagando en SAP correspondía a lo que se estaba abasteciendo en la flota.

🎯 Objetivo
Construir desde cero un proceso de conciliación mensual que:

Cruzara los registros de más de 2.000 abastecimientos/año entre TMS y SAP
Gestionara un volumen financiero de R$ 3,2 millones anuales
Identificara divergencias, pagos sin abastecimiento y abastecimientos sin factura
Produjera un dashboard ejecutivo en Power BI para seguimiento de la dirección
Quedara documentado en una Instrucción de Trabajo (IT) para garantizar la continuidad operacional


📊 Resultados
IndicadorValorVolumen financiero gestionado (2025–2026)R$ 3,2 millonesRegistros cruzados por ciclo anual2.000+Divergencias financieras identificadasR$ 638.000Vehículos activos monitorizados47 vehículosPuntos de suministro mapeados13 estacionesVolumen de combustible por año481.000+ litros
KPIs del último ciclo (enero–marzo 2026)

Total abastecimientos TMS: 296 registros / R$ 405.725,68
Total lanzamientos SAP: 352 registros / R$ 799.765,16
Conciliados: 107 pares confirmados / R$ 141.466,30
Divergencias encontradas: 13 casos / R$ 24.696,58
SAP sin correspondencia en TMS: 232 lanzamientos / R$ 633.602,28
TMS sin factura en SAP: 176 abastecimientos / R$ 239.563,60


🗂️ Estructura del Proyecto
conciliacao-combustiveis-tms-sap/
│
├── README.md                          ← Este archivo
├── IT_Conciliacion_Combustibles.pptx  ← Instrucción de Trabajo completa (14 slides)
├── Reporte_Combustible_2026.xlsx      ← Planilla de trabajo con todas las pestañas
│
└── docs/
    └── dashboard-preview.png          ← Captura del dashboard Power BI

🔧 Herramientas Utilizadas

Microsoft Excel — estructuración de las planillas de conciliación y tabla de nomenclatura
SAP (Módulo Financiero) — extracción del Libro Mayor (cuentas 05.1.1110101 y 05.1.1110104)
TMS — extracción de lanzamientos de combustible por establecimiento
Power BI — dashboard ejecutivo con KPIs de flota y conciliación
DAX — medidas calculadas para % conciliado, variación TMS vs SAP, ticket medio


📋 Cómo Funciona el Proceso
1. Extracción de datos
Los datos se exportan mensualmente de dos sistemas:

TMS → Excel: filtrando por establecimiento y período, eliminando registros revertidos
SAP → Excel: vía módulo Libro Mayor, utilizando únicamente la columna Débito

2. El desafío de los nombres de las estaciones
El mayor obstáculo técnico del proyecto: la misma estación física aparece con nombres completamente diferentes en los dos sistemas.
Nombre en TMSNombre en SAPPosto Gp BrasilJ.R.F.M COM DE COMBUSTIVEISE LUBRIFAuto Posto o CupimAUTO POSTO O CUPIM SAO JOSE LTDAPostos Mahle BrasilPostos Mahle Brasil Comercio de CombustiPichilauARLINDO DA FONSECA LINS & CIA LTDA
Solución creada: pestaña NOMENCLATURA DOS POSTOS — una tabla de correspondencia que funciona como diccionario entre los dos sistemas. Cada vez que un nombre no coincide, la tabla resuelve el conflicto antes de clasificar el registro.
3. Criterio de conciliación
Para cada lanzamiento del SAP, se busca en el TMS:

Valor igual o con diferencia de céntimos (tolerancia normal de redondeo)
Nombre de estación correspondiente (usando la tabla de correspondencia)
Fecha próxima (la factura puede emitirse días después del abastecimiento)

4. Clasificación de registros
EstadoSignificado✅ CONCILIADOPar confirmado en los dos sistemas — valor y estación correspondientes⚠️ DIVERGENCIAPar encontrado, pero valores diferentes — requiere investigación🔴 SAP s/conciliaciónLanzamiento en SAP sin abastecimiento en TMS — posible factura duplicada🔵 TMS s/conciliaciónAbastecimiento en TMS sin factura en SAP — normal para registros recientes
5. Reporte final y dashboard
El archivo Reporte_Combustible_2026.xlsx consolida todo en pestañas separadas por estado, con un Dashboard visual y una pestaña KPI con los principales indicadores del ciclo.

📝 Instrucción de Trabajo (IT)
Este proyecto incluye la documentación completa del proceso en formato de Instrucción de Trabajo — un documento de 14 slides creado para garantizar que cualquier analista del equipo pueda ejecutar la conciliación con precisión, incluso sin formación presencial.
La IT cubre:

Materiales necesarios y de dónde extraer cada archivo
Paso a paso detallado de extracción del TMS y del SAP
Cómo interpretar y filtrar las planillas antes de empezar
Cómo usar la tabla de nomenclatura de estaciones
Cómo clasificar cada registro y completar el reporte final


💡 Aprendizajes y Mejoras Futuras
Lo que funcionó bien:

La tabla de correspondencia de estaciones eliminó el 95% de los falsos negativos en la conciliación
La estructura de pestañas por estado hizo el análisis de divergencias mucho más ágil
El dashboard Power BI redujo el tiempo de presentación a la dirección de 1 hora a 15 minutos

Próximas mejoras planificadas:

 Automatizar el cruce con Python (pandas) para eliminar el proceso manual
 Crear alerta automática para divergencias superiores a R$ 500
 Conectar directamente vía API con el TMS para eliminar exportación manual
 Añadir análisis de consumo medio por vehículo (litros/km) para detectar anomalías


👤 Sobre la Autora
Isabelli Cristina Pereira da Silva
Analista de Datos · Business Intelligence · Gestión de Proyectos

📧 isabelli.c.p.silva@gmail.com
💼 linkedin.com/in/isabellicristina-silva
🐙 github.com/IsabelliCPSilva


Este proyecto fue desarrollado e implementado en entorno corporativo real. Los datos han sido anonimizados en este repositorio con fines de portafolio profesional.
