---
title: "Agregar y modificar datos de orígenes con el programa de instalación | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [ODBC], adding
- editing data sources [ODBC], ODBC driver for Oracle
- adding data sources [ODBC], ODBC driver for Oracle
- data sources [ODBC], changing
- data sources [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], adding data sources
ms.assetid: 54b2d61d-6ce5-45af-a776-e03180470ecf
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d7d077ab78f40b498ea7c43c7899c629e8eae5e3
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>Agregar y modificar orígenes de datos mediante el programa de instalación
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Un origen de datos identifica una ruta de acceso a datos que pueden incluir una biblioteca de red, servidor, base de datos y otros atributos: en este caso, el origen de datos es la ruta de acceso a una base de datos de Oracle. Para conectarse a un origen de datos, el Administrador de controladores comprueba el registro de Windows para obtener información de conexión específica.  
  
 Los controladores ODBC y el Administrador de controladores ODBC utiliza la entrada de registro creada por el Administrador de origen de datos de ODBC. Esta entrada contiene información sobre cada origen de datos y sus controladores asociados. Para poder conectarse a un origen de datos, su información de conexión debe agregarse al registro.  
  
 Para agregar y configurar orígenes de datos, use la [Administrador de orígenes de datos ODBC](../../odbc/admin/odbc-data-source-administrator.md). El Administrador de ODBC se actualiza la información de conexión del origen de datos. Agregar orígenes de datos, el Administrador de ODBC actualiza la información del registro.  
  
### <a name="to-add-a-data-source-for-windows"></a>Para agregar un origen de datos para Windows  
  
1.  Abra el Administrador de orígenes de datos ODBC.  
  
2.  En el cuadro de diálogo Administrador de orígenes de datos ODBC, haga clic en Agregar. Aparecerá el cuadro de diálogo Crear nuevo origen de datos.  
  
3.  Seleccione Microsoft ODBC para Oracle y, a continuación, haga clic en Finalizar. Aparece el ODBC de Microsoft para el cuadro de diálogo Configuración de Oracle.  
  
4.  En el cuadro Nombre de origen de datos, escriba el nombre del origen de datos que desea obtener acceso. Puede ser cualquier nombre que elija.  
  
5.  En el cuadro Descripción, escriba la descripción para el controlador. Este campo opcional describe el controlador de base de datos que se conecta el origen de datos. Puede ser cualquier nombre que elija.  
  
6.  En el cuadro Nombre de usuario, escriba su nombre de usuario de base de datos (el identificador de usuario de base de datos).  
  
7.  En el cuadro servidor, escriba el Alias de la base de datos o la cadena para el motor de servidor de Oracle que desea tener acceso de conexión.  
  
8.  Haga clic en Aceptar para agregar este origen de datos.  
  
> [!NOTE]  
>  Aparecerá el cuadro de diálogo de orígenes de datos y el Administrador de ODBC se actualiza la información de registro. El usuario el nombre y la cadena que ha escrito de conexión se convierten en los valores de conexión predeterminados para este origen de datos cuando se conecta a él.  
  
1.  Haga clic en Opciones establecer más especificaciones sobre el controlador ODBC para el programa de instalación de Oracle:  
  
    -   **Traducción** , haga clic en Seleccionar para elegir un traductor de datos cargados. El valor predeterminado es \<traductor n >.  
  
    -   **Rendimiento** : la sección de comentarios de incluir en la casilla de verificación de funciones de catálogo especifica si el controlador devuelve columnas de la sección Comentarios para el [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) conjunto de resultados. El controlador ODBC para Oracle proporciona un acceso más rápido si no se establece este valor.  
  
         Los SINÓNIMOS de incluir en la casilla de verificación de las columnas de SQL especifica si el controlador devuelve información de columna. **Tamaño de búfer** especifica el tamaño, en bytes, asignada para recibir los datos capturados. El controlador optimiza la recuperación así que una búsqueda desde el servidor Oracle devuelve las filas suficientes para rellenar un búfer del tamaño especificado. Los valores más grandes tienden a aumentar el rendimiento al capturar una gran cantidad de datos.  
  
    -   **Personalización** : The exigir ODBC estándar DayOfWeek de casilla de verificación Especifica si el conjunto de resultados se se ajusta al formato de día de la semana especificado de ODBC (el domingo = 1; El sábado = 7). Si esta casilla de verificación está desactivada, se devuelve el valor de Oracle específica de la configuración regional.  
  
         El SQLDescribeCol **siempre devuelve un valor de precisión** casilla de verificación Especifica si el controlador debería devolver un valor distinto de cero para la *cbColDef* argumento de **SQLDescribeCol**. Este atributo de cadena de conexión se aplica únicamente a las columnas donde no hay escala definido de Oracle, como calcular numéricas columnas y columnas definidas como NUMBER sin precisión o escala. A **SQLDescribeCol** llamar devuelve 130 para la precisión cuando Oracle no proporciona dicha información. Si esta casilla de verificación está desactivada, el controlador devolverá 0 para estos tipos de columnas.  
  
2.  Haga clic en Agregar para agregar otro origen de datos, o haga clic en Cerrar para salir.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Para modificar un origen de datos de Windows  
  
1.  Abra el Administrador de orígenes de datos ODBC. Haga clic en la ficha DSN correspondiente.  
  
2.  Seleccione el origen de datos de Oracle que desea modificar y, a continuación, haga clic en configurar. Aparece el ODBC de Microsoft para el cuadro de diálogo Configuración de Oracle.  
  
3.  Modifique los campos de origen de datos aplicable y, a continuación, haga clic en Aceptar.  
  
 Cuando haya terminado de modificar la información de este cuadro de diálogo, el Administrador de ODBC actualiza la información de registro.
