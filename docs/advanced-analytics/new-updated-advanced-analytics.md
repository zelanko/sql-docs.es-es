---
title: 'Actualizado: Advanced Analytics para documentos de SQL Server | Documentos de Microsoft'
description: "Mostrar fragmentos de contenido actualizado para recientemente modificadas en documentación, Advanced Analytics para Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.workload: advanced-analytics
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: fb6185aae04a1fb53a4db03cbab267e3f52dc779
ms.contentlocale: es-es
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>Nuevos y actualizados recientemente: análisis avanzados para SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **2017-07-18** &nbsp; - a - &nbsp; **2017-09-11**
- *Área de asunto:* &nbsp; **Advanced Analytics para SQL Server**.

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Cómo realizar la puntuación en tiempo real o puntuación nativo de SQL Server](r/how-to-do-realtime-scoring.md)
2. [Instalar previamente entrenado máquina aprendizaje de los modelos en SQL Server](r/install-pretrained-models-sql-server.md)
3. [Puntuación nativa](sql-native-scoring.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

Esta sección muestra los extractos de las actualizaciones que se recopilan de los artículos que se han producido recientemente una actualización a gran escala.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

Esta lista compact proporciona vínculos a todos los artículos actualizados que se enumeran en la sección de citas.

1. [Configurar los servicios de aprendizaje de máquina de Python (In-Database)](#TitleNum_1)
2. [Introducción a revoscalepy](#TitleNum_2)
3. [Diferencias en las características de aprendizaje automático entre las ediciones de SQL Server](#TitleNum_3)
4. [Incorporación de operatividad a código de R (servicios de aprendizaje de máquina)](#TitleNum_4)
5. [Rendimiento de los servicios de R: resultados y recursos](#TitleNum_5)
6. [Rendimiento de R Services: optimización de datos](#TitleNum_6)
7. [Administración de paquetes de R para SQL Server](#TitleNum_7)
8. [Configurar SQL Server Machine Learning Services (en base de datos)](#TitleNum_8)
9. [Configuración de SQL Server para su uso con R](#TitleNum_9)
10. [Ajuste del rendimiento de R en SQL Server](#TitleNum_10)
11. [Escenarios de ciencia de datos y plantillas de soluciones](#TitleNum_11)
12. [Novedades en servicios de aprendizaje de máquina en SQL Server](#TitleNum_12)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-set-up-python-machine-learning-services-in-databasepythonsetup-python-machine-learning-servicesmd"></a>1. &nbsp;[Configurar servicios de aprendizaje de máquina de Python (In-Database)](python/setup-python-machine-learning-services.md)

*Actualizado: 2017-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([siguiente](#TitleNum_2))

<!-- Source markdown line 263.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 fbe2ef55a5caecd64bb21ce854617a10b2d65567 8cd65baf77f27db00a0a4f07f3129a4231edb48b  (PR=3084  ,  Filename=setup-python-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=05976158e43d7dfafaf02289462d1537f5beeb36) -->



     [Modify the user account pool for SQL Server R Services--../r/modify-the-user-account-pool-for-sql-server-r-services.md)

Si está usando SQL Server Standard Edition y no tiene el regulador de recursos, puede usar vistas de administración dinámica y eventos extendidos para ayudarle a administrar los recursos de servidor. También puede usar la supervisión de eventos de Windows para este propósito. Para obtener más información, consulte [supervisión y administración R Services--.. /r/Managing-and-Monitoring-r-Solutions.MD).

**Actualizar los componentes de aprendizaje automático**


Al instalar servicios de aprendizaje de máquina mediante SQL Server 2017, obtendrá la versión de los componentes en el momento en que se publicó la versión. Cada vez que aplicar la revisión o actualiza la instancia de SQL Server, los componentes de aprendizaje de máquina se actualizan también.

Puede actualizar los componentes de forma más rápida que se admite de aprendizaje automático en versiones de SQL Server, al instalar servidor de aprendizaje de máquina de Microsoft. Si lo hace, también obtendrá las nuevas características que se admite en la versión más reciente del servidor de aprendizaje de máquina, como:

+ Las actualizaciones de paquetes de Python para [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) y [microsoftml para Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).
+ [Previamente entrenada modelos](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) para el análisis de clasificación y el texto de la imagen.

Para obtener información acerca de cómo actualizar una instancia, vea [R Actualizar componentes a través de enlace--.. \r\use-sqlbindr-exe-to-Upgrade-an-Instance-of-SQL-Server.MD).

> [!NOTE]
>
> La versión actual contiene la versión más reciente de todos los componentes de aprendizaje de máquina. Por lo tanto, aunque se admiten las actualizaciones a través del servidor de aprendizaje de máquina de Microsoft para SQL Server 2017, la actualización que está disponible actualmente solo se aplica a instancias de SQL Server 2016.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-introducing-revoscalepypythonwhat-is-revoscalepymd"></a>2. &nbsp;[Introducción revoscalepy](python/what-is-revoscalepy.md)

*Actualizado: 2017-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [siguiente](#TitleNum_3))

<!-- Source markdown line 79.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 33f4e0e2421fa79fc11931dc7f29bff4432c6f5a d2eac3313a74bc5d5afd754fc357b3693e6801e1  (PR=2939  ,  Filename=what-is-revoscalepy.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



| (column_1) | (Columna_2) | (column_3) |
| :-- | :-- | :-- |
|`rx_btrees` | Árboles de decisión incrementados de gradiente estocástico ajuste|`rx_btrees_ex`en CTP 2.0|
|`rx_dforest` | Bosques de decisión de clasificación y regresión de ajuste|`rx_dforest_ex`en CTP 2.0|
|`rx_dtree` | Ajuste de los árboles de clasificación y regresión |`rx_dtree_ex`en CTP 2.0|
|`rx_lin_mod` | Crear un modelo lineal|`rx_lin_mod_ex`en CTP 2.0|
|`rx_logit` | Crear un modelo de regresión logística|`rx_logit_ex`en CTP 2.0|
|`rx_predict` | Generar predicciones de un modelo entrenado|`rx_predict_ex`en CTP 2.0|
|`rx_summary` | Generar un resumen del modelo||

Nuevos algoritmos de aprendizaje automático también se proporcionan con la versión de Python de [MicrosoftML](https://docs.microsoft.com/en-us/r-server/python-reference/microsoftml/microsoftml-package):

| Función| Description|
| ------ | ------ |
|`rx_fast_forest` |Crea un modelo de bosque de decisión|
|`rx_fast_linear` | Regresión lineal con estocástico ascenso coordenada dual|
|`rx_fast_trees` | Crear un modelo de árbol incrementado |
|`rx_logistic_regression` | Crear un modelo de regresión logística|
|`rx_neural_network` | Crear un modelo de red neuronal personalizable |
|`rx_oneclass_svm` | Crea un modelo SVM en un conjunto de datos equilibrado, para su uso en la detección de anomalías|

> [!TIP]
> Muchos de estos algoritmos ya se proporcionan como módulos de aprendizaje automático de Azure.

MicrosoftML para Python también incluye una serie de transformaciones y funciones auxiliares, como:

+ `rx_predict`genera predicciones a partir de un modelo entrenado y puede usarse para puntuar en tiempo real
+ funciones de características de imagen
+ funciones para la extracción de opiniones y procesamiento de texto

Para obtener más información, vea [Introducción a MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> La Comunidad de Python usa las convenciones de codificación que pueden ser distintas del que está acostumbrado, incluidas todas las letras en minúsculas y caracteres de subrayado en lugar de grafía camel para los nombres de parámetro. Además, puede ser haya observado que el **revoscalepy** biblioteca siempre está en minúscula. ¡Así es! Otra convención de Python.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-differences-in-machine-learning-features-between-editions-of-sql-serverrdifferences-in-r-features-between-editions-of-sql-servermd"></a>3. &nbsp;[Diferencias en las características de aprendizaje de máquina entre las ediciones de SQL Server](r/differences-in-r-features-between-editions-of-sql-server.md)

*Actualizado: 2017-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2) | [siguiente](#TitleNum_4))

<!-- Source markdown line 47.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5890e212063f3ef228e69afe54e226320d2467f 4e0357701d960c0b8dbda1ac8d56a82f3335c77f  (PR=2964  ,  Filename=differences-in-r-features-between-editions-of-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=7b4f037616e0559ac62bbae5dbe04aeffe529b06) -->



     Only Express Edition with Advanced Services includes the machine learning features. The performance limitations are similar to Standard Edition. Web edition is not intended for tasks such as creating machine learning models; however, you can use the PREDICT function to perform scoring using models trained elsewhere.

-   **Azure SQL Database**

     Características de aprendizaje de máquina, como R y Python secuencias de comandos no se admiten en la base de datos de SQL Azure.

     Para obtener más información y anuncios acerca de cuándo estará disponible, esta característica, consulte el blog de SQL Server: [Python en SQL Server 2017: mejorada de aprendizaje automático en bases de datos](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)


**Idiomas admitidos en todas las ediciones**


Se admiten los siguientes idiomas de aprendizaje de máquina para todas las ediciones:

+ SQL Server de 2017: R y Python
+ SQL Server 2016: R solo

Microsoft R Open se incluye con todas las ediciones.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-operationalize-r-code-machine-learning-servicesroperationalizing-your-r-codemd"></a>4. &nbsp;[Código de incorporación de operatividad a R (servicios de aprendizaje de máquina)](r/operationalizing-your-r-code.md)

*Actualizado: 2017-07-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3) | [siguiente](#TitleNum_5))

<!-- Source markdown line 56.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7e11d9a5db93932ec89ca96b5337aa4ea03c1d13 0779f06444b5b73ae2dff8bc190d0e388b4ae8e7  (PR=2660  ,  Filename=operationalizing-your-r-code.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=70a1fd4dbec68d22187585de69a1d603c39e259e) -->



+ [En tiempo real:.. / real tiempo scoring.md) de puntuación, optimizado para los lotes pequeños
+ Puntuación, para llamar desde una aplicación de varias filas
+ [Nativo puntuación--.. / scoring.md de nativo de sql), para la predicción por lotes rápidamente desde SQL Server sin llamar a R

Este tutorial proporciona ejemplos de puntuación mediante un procedimiento almacenado en el lote y modos de fila:

+ [Finalizar para terminar el tutorial de ciencia de datos para R en SQL Server:.. / tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

Vea estas plantillas de solución para obtener ejemplos de cómo integrar en una aplicación de puntuación:

+ [Previsión de comercio minorista](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [Detección de fraudes](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)
+ [Cliente de agrupación en clústeres](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

**Mejorar el rendimiento y la escala**


Aunque el lenguaje de código abierto R se sabe que tienen limitaciones, el paquete RevoScaleR API pueden operar en conjuntos de datos grandes y aprovechar los cálculos en bases de datos de varios subprocesos, de varios núcleos, varios procesos de.

Si la solución R usa agregaciones complejas o implica grandes conjuntos de datos, puede aprovechar altamente eficientes agregaciones en memoria e índices de almacén de columnas de SQL Server y dejar que el código R controle los cálculos estadísticos y de puntuación.

Para obtener más información acerca de cómo mejorar el rendimiento en el aprendizaje automático de SQL Server, vea:

+ [Optimización de rendimiento para SQL Server R Services--.. /.. / advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [Sugerencias y trucos para la optimización de rendimiento](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Adapta el código de R para otras plataformas o contextos de proceso**




&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-performance-for-r-services-results-and-resourcesrperformance-case-study-r-servicesmd"></a>5. &nbsp;[Rendimiento para los servicios de R: resultados y recursos](r/performance-case-study-r-services.md)

*Actualizado: 2017-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_4) | [siguiente](#TitleNum_6))

<!-- Source markdown line 282.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 40c8cd255ead88edc60531d45dd0377ecbaf7c9b eeca5eed96e2223508910b246dbff18173eecea3  (PR=2565  ,  Filename=performance-case-study-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



Los paquetes RevoScaleR y de MicrosoftML se usaron para entrenar un modelo de predicción en una solución de R complejo que implican grandes conjuntos de datos. Las consultas SQL y código de R son idénticos. Todas las pruebas se realizaron en una sola máquina virtual de Azure con SQL Server instalado. El autor, a continuación, en comparación con tiempos de puntuación con y sin estas optimizaciones proporcionadas por SQL Server:

- Tablas en memoria
- Soft-NUMA
- Regulador de recursos

Para evaluar el efecto de NUMA de software en la ejecución del script de R, el equipo de ciencia de datos probado la solución en una máquina virtual con 20 núcleos físicos. En estos núcleos físicos, cuatro nodos NUMA de software se crearon automáticamente, tal que cada nodo contiene cinco núcleos.

Afinamiento de CPU se aplica en el escenario de coincidencia de reanudación, para evaluar el impacto sobre los trabajos de R. Cuatro **grupos de recursos SQL** y cuatro **grupos de recursos externos** fueron creadas, y no se especificó la afinidad de CPU para asegurarse de que se utilizaría el mismo conjunto de CPU en cada nodo.

Cada uno de los grupos de recursos se asignó a un grupo de cargas de trabajo diferente, para optimizar el uso de hardware. El motivo es que Soft-NUMA y afinidad de CPU no puede dividir la memoria física en los nodos NUMA físicos; por lo tanto, por definición todos los nodos NUMA automáticos que se basan en el mismo nodo NUMA físico deben usar memoria en el mismo bloque de memoria de sistema operativo. En otras palabras, no hay ninguna afinidad de procesador de memoria.

El siguiente proceso se usó para crear esta configuración:

1. Reducir la cantidad de memoria asignada de forma predeterminada en SQL Server.

2. Cree cuatro grupos nuevos para ejecutar los trabajos de R en paralelo.

3. Cree cuatro grupos de cargas de trabajo de forma que cada grupo de cargas de trabajo está asociado a un grupo de recursos.

4. Reinicie el regulador de recursos con los nuevos grupos de cargas de trabajo y las asignaciones.

5. Crear una función clasificadora definida por el usuario (UDF) para asignar diferentes tareas en los grupos de cargas de trabajo diferente.

6. Actualizar la configuración del regulador de recursos para usar la función para los grupos de cargas de trabajo adecuado.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-performance-for-r-services---data-optimizationrr-and-data-optimization-r-servicesmd"></a>6. &nbsp;[Rendimiento para R Services: optimización de datos](r/r-and-data-optimization-r-services.md)

*Actualizado: 2017-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_5) | [siguiente](#TitleNum_7))

<!-- Source markdown line 107.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2ae2e54e8c5c8a3ec92fd2017088dd6ee879a9a1 9cb06bdce4ad6dfa2e9dc19da49103a6cd9817b3  (PR=2565  ,  Filename=r-and-data-optimization-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



> Si se especifica una tabla en el origen de datos en lugar de una consulta, R Services usa heurística interna para determinar las columnas necesarias para capturar de la tabla. Sin embargo, este enfoque es poco probable que resulta en que la ejecución en paralelo.

Para asegurarse de que se pueden analizar los datos en paralelo, la consulta utilizada para recuperar los datos debe configurarse de tal manera que el motor de base de datos puede crear un plan de consulta en paralelo. Si el código o el algoritmo utiliza grandes volúmenes de datos, asegúrese de que la consulta da a `RxSqlServerData` está optimizado para la ejecución en paralelo. Una consulta que no da como resultado un plan de ejecución en paralelo puede producir un único proceso para el cálculo.

Si necesita trabajar con grandes conjuntos de datos, use Management Studio o el otro analizador de consultas SQL antes de ejecutar código R, para analizar el plan de ejecución. A continuación, tome las medidas recomendadas para mejorar el rendimiento de la consulta. Por ejemplo, un índice que falta en una tabla puede afectar al tiempo necesario para ejecutar una consulta. Para obtener más información, consulte [Monitor y debería ajustar para obtener un rendimiento--.. /.. / relational-databases/performance/monitor-and-tune-for-performance.md).

Otro error común que puede afectar al rendimiento es que una consulta recupera columnas de más de los necesarios. Por ejemplo, si una fórmula se basa en solo tres columnas, pero la tabla de origen tiene 30 columnas, va a mover datos innecesariamente.

 + Evite el uso de `SELECT *`!
 + Tardar algún tiempo para revisar las columnas del conjunto de datos e identificar solo los necesarios para el análisis
 + Quite las consultas de las columnas que contienen tipos de datos que no son compatibles con el código de R, tales como GUID y rowguid
 + Comprobación de no compatible formatos de fecha y hora
 + En lugar de cargar una tabla, crear una vista que selecciona ciertos valores o convierte columnas para evitar errores de conversión

**Optimizar el algoritmo de aprendizaje de máquina**


Esta sección proporciona varias sugerencias y recursos que son específicos de RevoScaleR y otras opciones de Microsoft R.



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-r-package-management-for-sql-serverrr-package-management-for-sql-server-r-servicesmd"></a>7. &nbsp;[Administración de paquetes de R para SQL Server](r/r-package-management-for-sql-server-r-services.md)

*Actualizado: 2017-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_6) | [siguiente](#TitleNum_8))

<!-- Source markdown line 22.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2add5a7e1aef02487ac875e353c51161658050a4 5da92dd8b5402266a837172bda9aaabed3162ce8  (PR=2939  ,  Filename=r-package-management-for-sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



En este tema se describe las características de administración de paquetes que puede usar para administrar paquetes de R que se ejecutan en una instancia de SQL Server.

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

**Administración de paquetes mediante T-SQL**


Puede continuar con la instalación de paquetes de R como administrador en el equipo, si tiene los privilegios, y si es la única persona que utiliza el servidor para trabajos de aprendizaje de máquina.

Sin embargo, si tiene que compartir paquetes con otros usuarios, o si necesitan varias personas ejecutar trabajos de aprendizaje de máquina en el servidor, es más eficaz para configurar una biblioteca compartida de paquete. SQL Server admite esto a través de roles de base de datos.

El Administrador de base de datos es responsable de establecer los roles y agregar usuarios a los roles. A través de roles, el Administrador de base de datos puede controlar quién tiene permiso para agregar o quitar paquetes de R desde el entorno de SQL Server y puede auditar la instalación del paquete.

**Roles de base de datos de administración de paquetes**


Los siguientes nuevos roles de base de datos admiten la seguridad de la instalación y administración de paquetes de R en SQL Server:

- `rpkgs-users`: Permite a los usuarios utilizar los paquetes compartidos que se instalaron los miembros de los `rpkgs-shared` rol.

- `rpkgs-private`: Proporciona acceso a los paquetes compartidos con los mismos permisos que los `rpkgs-users` rol. Los miembros de este rol también pueden instalar, quitar y usar paquetes de ámbito privado.

-  `rpkgs-shared`: Proporciona los mismos permisos que los `rpkgs-private` rol. Los usuarios que son miembros de este rol también pueden instalar o quitar paquetes compartidos.

- `db_owner`: Tiene los mismos permisos que los `rpkgs-shared` rol. También puede conceder a los usuarios el derecho de instalar o quitar paquetes compartidos y privados.

**Crear una biblioteca de paquete externo mediante T-SQL**


Además, SQL Server 2017 es compatible con la instrucción T-SQL, **crear biblioteca externa**, para admitir la administración de administrador de base de datos de bibliotecas externas. Actualmente se puede utilizar esta instrucción para crear bibliotecas basadas en Windows para R. adicionales soporte técnico está planeada en el futuro para los paquetes de Python y para los paquetes que se escriben para su ejecución en otras plataformas, como Linux.



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-set-up-sql-server-machine-learning-services-in-databaserset-up-sql-server-r-services-in-databasemd"></a>8. &nbsp;[Configurar servicios de aprendizaje de máquina de SQL Server (In-Database)](r/set-up-sql-server-r-services-in-database.md)

*Actualizado: 2017-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_7) | [siguiente](#TitleNum_9))

<!-- Source markdown line 240.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 452dc36b4d0097f9562642238ba49eea0373d25b 4d355f6494b417dd90dce3943e7176eaece7336e  (PR=3070  ,  Filename=set-up-sql-server-r-services-in-database.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



Si crea una solución en R en un equipo cliente de ciencia de datos y que necesite ejecutar código con el equipo de SQL Server como el contexto de proceso, puede utilizar un inicio de sesión SQL o la autenticación integrada de Windows.

* En caso de usar un inicio de sesión de SQL: asegúrese de que el inicio de sesión tenga los permisos adecuados en la base de datos donde se van a leer los datos. Puede hacerlo agregando *conectarse a* y *seleccione* permisos, o agregando el inicio de sesión para la *db_datareader* rol. Para los inicios de sesión que necesitan para crear objetos, agregue *funciones DDL_admin* derechos. Para los inicios de sesión que deben guardar los datos en tablas, agregue el inicio de sesión para la *db_datawriter* rol.

* Para la autenticación de Windows: tendrá que configurar un origen de datos ODBC en el cliente de ciencia de datos que especifica el nombre de instancia y otra información de conexión. Para obtener más información, consulte [Administrador de orígenes de datos ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator).

**Pasos siguientes**


Después de comprobar que funciona la característica de ejecución del script en SQL Server, puede ejecutar comandos de R y Python desde SQL Server Management Studio, código de Visual Studio o cualquier otro cliente que puede enviar instrucciones T-SQL en el servidor.

Sin embargo, puede realizar algunos cambios en la configuración del sistema para admitir un uso intensivo de aprendizaje automático, o agregar nuevos paquetes de R.

Esta sección enumeran algunas modificaciones comunes que puede realizar para admitir el aprendizaje automático.

**Agregue más cuentas de trabajo**


Si cree que podría usar R mucho, o si se espera que muchos usuarios pueden ejecutar scripts al mismo tiempo, puede aumentar el número de cuentas de trabajo que están asignadas al servicio Launchpad. Para obtener más información, consulte [modificar el grupo de cuentas de usuario de SQL Server R Services--modify-the-user-account-pool-for-sql-server-r-services.md).

**<a name="bkmk_optimize"></a>Optimizar el servidor para la ejecución de scripts externos**




&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-sql-server-configuration-for-use-with-rrsql-server-configuration-r-servicesmd"></a>9. &nbsp;[Configuración de SQL Server para su uso con R](r/sql-server-configuration-r-services.md)

*Actualizado: 2017-07-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_8) | [siguiente](#TitleNum_10))

<!-- Source markdown line 149.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3f57bae70e3c118c1e2bcd57017322940bae83f8 f296242d470db47077cba4215ef420bd0c60bf33  (PR=2660  ,  Filename=sql-server-configuration-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=70a1fd4dbec68d22187585de69a1d603c39e259e) -->



Si la consulta devuelve un único nodo de memoria (nodo 0), no tiene NUMA de hardware o el hardware está configurado como intercalado (no NUMA). SQL Server también omite NUMA de hardware cuando hay cuatro o menos CPU, o si al menos un nodo tiene únicamente una CPU.

Si el equipo tiene varios procesadores, pero no tiene NUMA de hardware, también puede usar [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) para subdividir CPU en grupos más pequeños.  En SQL Server 2016 y 2017 de SQL Server, la característica Soft-NUMA se habilita automáticamente al iniciar el servicio de SQL Server.

Cuando se habilita Soft-NUMA, SQL Server administra automáticamente los nodos en su nombre; Sin embargo, para optimizar cargas de trabajo específicas, puede deshabilitar _la afinidad parcial_ y configurar manualmente la afinidad de CPU para los nodos NUMA de software. Esto puede proporcionarle más control sobre el que se asignan las cargas de trabajo a otros nodos, especialmente si está usando una edición de SQL Server que admite regulador de recursos. Al especificar la afinidad de CPU y Alinear grupos de recursos con grupos de CPU, puede reducir la latencia y garantizar que los procesos relacionados se realizan en el mismo nodo NUMA.

El proceso general de configuración de NUMA de software y la afinidad de CPU para admitir las cargas de trabajo de R es el siguiente:

1. Habilitar soft-NUMA, si está disponible
2. Definir la afinidad del procesador
3. Crear grupos de recursos para los procesos externos, con [regulador de recursos--.. /r/Resource-Governance-for-r-Services.MD)
4. Asigne a los [grupos de cargas de trabajo..: /.. / relational-databases/resource-governor/resource-governor-workload-group.md) a determinados grupos de afinidad

Para obtener más información, incluido el código de ejemplo, vea este tutorial: [SQL optimización sugerencias y trucos (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Otros recursos:**



&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-performance-tuning-for-r-in-sql-serverrsql-server-r-services-performance-tuningmd"></a>10. &nbsp;[Ajuste del rendimiento de R en SQL Server](r/sql-server-r-services-performance-tuning.md)

*Actualizado: 2017-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_9) | [siguiente](#TitleNum_11))

<!-- Source markdown line 76.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9c30753efdec81e499d5654b5b7a07f0cfe5b003 136a9f483bc8c9e1f69cf9d340d1472c21a52ec4  (PR=2565  ,  Filename=sql-server-r-services-performance-tuning.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



- Configurar la instancia de SQL Server para las operaciones del motor de base de datos de equilibrio y R o en los niveles adecuados de la ejecución del script de Python. Esto puede incluir cambiar valores predeterminados de SQL Server para la memoria y uso de CPU, NUMA y configuración de la afinidad de procesador y creación de grupos de recursos.

- Optimizar el equipo del servidor para admitir un uso eficaz de scripts externos. Esto puede incluir el aumento del número de cuentas que se usan para la ejecución de scripts externos, habilitar la administración de paquetes, y relacionados con la asignación de usuarios a roles de seguridad.

- Aplicar las optimizaciones específicas para el almacenamiento de datos y la transferencia en SQL Server, incluida la indización y las estrategias de estadísticas, diseño de la consulta y optimización de consultas y el diseño de tablas que se usan para el aprendizaje automático. También puede analizar los orígenes de datos y datos de métodos de transporte, o modificar los procesos ETL para optimizar la extracción de características.

- Optimizar el modelo analítico para evitar las ineficiencias. El ámbito de las optimizaciones que son posibles dependen de la complejidad de su código en R y los paquetes y los datos que se utiliza. Tareas clave incluyen lo que elimina las transformaciones de datos costosas o descargar datos preparación o característica ingeniería las tareas de R o Python para procesos ETL o SQL. También podría refactorizar las secuencias de comandos, eliminar la instalación de paquete en línea, dividir código R en procedimientos independientes para el entrenamiento, la puntuación y evaluación o simplificar el código para que funcione de forma más eficaz que un procedimiento almacenado.

**Artículos de esta serie**


+ [Ajuste del rendimiento de R en SQL Server - hardware--.. \r\sql-Server-Configuration-r-Services.MD)

    Proporciona instrucciones para configurar el hardware que..! CLUIR-NotShown--ssNoVersion_md--... \..\includes\ssnoversion-md.md)] se instala en y para configurar la instancia de SQL Server para admitir mejor scripts externos. Es especialmente útil para **los administradores de base de datos**.

+ [Ajuste del rendimiento de R en SQL Server: optimización del código y datos--.. \r\r-and-Data-Optimization-r-Services.MD)



&nbsp;

&nbsp;

---

<a name="TitleNum_11"/>

### <a name="11-nbsp-data-science-scenarios-and-solution-templatestutorialsdata-science-scenarios-and-solution-templatesmd"></a>11. &nbsp;[Escenarios de ciencia de datos y plantillas de solución](tutorials/data-science-scenarios-and-solution-templates.md)

*Actualizado: 2017-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_10) | [siguiente](#TitleNum_12))

<!-- Source markdown line 45.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 22c621731015f2192cb0b8d61b22062a4be50e70 6cf9e3f0a3803ed2bce9c4ffadfd7314f15f6b51  (PR=2964  ,  Filename=data-science-scenarios-and-solution-templates.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=7b4f037616e0559ac62bbae5dbe04aeffe529b06) -->



[Predecir cómo y cuándo ponerse en contacto con clientes potenciales](https://microsoft.github.io/r-server-campaign-optimization/)

**¿Qué:** esta solución usa datos de la industria de seguros para predecir la clientes potenciales basadas en datos demográficos, los datos históricos de respuesta y detalles específicos del producto.  También se generaron las recomendaciones para indicar la mejor canal y hora a los usuarios de enfoque para influir en el comportamiento de compra.

**Cómo:** la solución se crea y se compara varios modelos. La solución también muestra la integración de datos automatizada y la preparación de datos mediante procedimientos almacenados. Se proporcionan ejemplos paralelas para SQL Server en bases de datos, en Azure y HDInsight Spark.

**Atención: predecir permanencia en el hospital**


[Predecir permanencia en el hospital](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**¿Qué:** predecir con exactitud qué pacientes pueden requerir hospitalización a largo plazo es una parte importante de atención y planificación. Los administradores deben poder determinar qué funciones requieren más recursos y proveedores de atención médica desea garantizar que pueden satisfacer las necesidades de los pacientes.

**Cómo:** esta solución usa la máquina Virtual de ciencia de datos e incluye una instancia de SQL Server con aprendizaje automático habilitado. También incluye un conjunto de informes de Power BI que puede usar para interactuar con un modelo implementado.

**Renovación de cliente**


[Plantilla de predicción de renovación de cliente (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)

**¿Qué:** analizar y predecir la renovación del cliente es importante en cualquier sector donde debe administrarse y evitar la pérdida de los clientes a competidores: banca, telecomunicaciones y comercial, por nombrar algunos. El objetivo del análisis del abandono es identificar qué clientes tienen probabilidades de abandonar y después adoptar las acciones adecuadas para conservar a esos clientes y mantener su negocio.



&nbsp;

&nbsp;

---

<a name="TitleNum_12"/>

### <a name="12-nbsp-whats-new-in-machine-learning-services-in-sql-serverwhat-s-new-in-sql-server-machine-learning-servicesmd"></a>12. &nbsp;[Cuáles son las novedades en servicios de aprendizaje de máquina en SQL Server](what-s-new-in-sql-server-machine-learning-services.md)

*Actualizado: 2017-08-02* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_11))

<!-- Source markdown line 33.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 025e68a93895a3788a63847cd91bff068775acf3 6dc0be2920c670235038a126d135e08d6f16ec3a  (PR=2712  ,  Filename=what-s-new-in-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=ea75391663eb4d509c10fb785fcf321558ff0b6e) -->



> Servicios de aprendizaje de máquina, incluido el uso de R o Python, no se admiten cuando se ejecuta SQL Server en Linux o en la base de datos SQL de Azure. Buscar cambios en una versión posterior.
>
> Sin embargo, la puntuación nativo mediante la función de PREDICCIÓN se admite actualmente en la edición de Linux.

**Integración de Python en bases de datos**


Puede ejecutar Python en procedimientos almacenados, o ejecutar de forma remota con el equipo de SQL Server como el contexto de ejecución de Python. Esta integración se abre nuevos caminos para la amplia comunidad de Python a los desarrolladores y los datos científicos aprovechar la eficacia de SQL Server y para explorar las innovaciones de Microsoft como **revoscalepy** y **microsoftml**.

Los desarrolladores de SQL Server obtienen acceso a las bibliotecas de Python amplia desde el ecosistema de código abierto, incluidos los marcos conocidos como scikit-obtener, Tensorflow, Caffe y Theano/Keras.

Pero se ejecuta en bases de datos no es solo para; de aprendizaje automático de Python hay una gran cantidad de otras aplicaciones posibles para la integración de Python con SQL, aprovechando las ventajas de los lenguajes respectivos para entregar soluciones más inteligentes y eficaces.

+ **revoscalepy**

    Esta versión incluye la versión final de **revoscalepy**, lo que proporciona Pythonic equivalentes de escalable, algoritmos de RevoScaleR de transmisión por secuencias. Puede crear modelos de Python para las regresiones lineales y logísticas, árboles de decisión, los árboles impulsados y bosques aleatorios, paralelizar todas y puede que se ejecutan en contextos de proceso remoto.

    Para obtener más información, consulte [What ' s revoscalepy--python/what-es-revoscalepy.md).

+ Contextos de proceso remoto de Python

    Esta versión admite el uso de varios orígenes de datos y contextos de proceso remoto. El científico de datos o el desarrollador puede ejecutar código Python en un servidor SQL Server remoto, para explorar datos o crear modelos sin mover los datos. El uso de contextos de proceso remoto requiere **revoscalepy**.







## <a name="similar-articles"></a>Artículos similares

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

En esta sección se enumera los artículos muy similar para los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas con artículos nuevos o actualizados recientemente

- [Nuevos y actualizados (3 + 12): **Advanced Analytics para SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos y actualizados (5 + 0): **conectar con SQL Server** documentos](../connect/new-updated-connect.md)
- [Nuevos y actualizados (5 + 1): **motor de base de datos de SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Nuevos y actualizados (19 + 82): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Nuevos y actualizados (1 + 8): **Linux para SQL** documentos](../linux/new-updated-linux.md)
- [Nuevos y actualizados (12 + 1): **bases de datos relacionales de SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Nuevos y actualizados (0 + 1): **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Nuevos y actualizados (7 + 1): **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Nuevos y actualizados (1 + 1): **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Nuevos y actualizados (0 + 2): **SQL Server Migration Assistant (SSMA)** documentos](../ssma/new-updated-ssma.md)
- [Nuevos y actualizados (1 + 4): **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Nuevos y actualizados (4 + 1): **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)
- [Nuevos y actualizados (0 + 1): **Tools para SQL** documentos](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas sin artículos nuevos ni actualizados recientemente

- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos y actualizados (0 + 0): **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos y actualizados (0 + 0): **Master Data Services (MDS) para SQL** documentos](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + Actualizados (0+0): documentos de **Ejemplos para SQL**](../sample/new-updated-sample.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)



