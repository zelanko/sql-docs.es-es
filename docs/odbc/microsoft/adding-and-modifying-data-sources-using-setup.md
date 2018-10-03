---
title: Agregar y modificar datos orígenes mediante el programa de instalación | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], adding
- editing data sources [ODBC], ODBC driver for Oracle
- adding data sources [ODBC], ODBC driver for Oracle
- data sources [ODBC], changing
- data sources [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], adding data sources
ms.assetid: 54b2d61d-6ce5-45af-a776-e03180470ecf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 28f7fb52cb4babdce6e90452f40d81ba643466ea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767763"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>Agregar y modificar orígenes de datos mediante el programa de instalación
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 Un origen de datos identifica una ruta de acceso a los datos que pueden incluir una biblioteca de red, servidor, base de datos y otros atributos, en este caso, el origen de datos es la ruta de acceso a una base de datos de Oracle. Para conectarse a un origen de datos, el Administrador de controladores comprueba el registro de Windows para obtener información de conexión específica.  
  
 Los controladores ODBC y el Administrador de controladores ODBC utiliza la entrada de registro creada por el Administrador de origen de datos ODBC. Esta entrada contiene información sobre cada origen de datos y sus controladores asociados. Antes de poder conectarse a un origen de datos, su información de conexión debe agregarse al registro.  
  
 Para agregar y configurar orígenes de datos, utilice el [Administrador de orígenes de datos ODBC](../../odbc/admin/odbc-data-source-administrator.md). El Administrador de ODBC se actualiza la información de conexión del origen de datos. Agregar orígenes de datos, el Administrador de ODBC actualiza la información del registro.  
  
### <a name="to-add-a-data-source-for-windows"></a>Para agregar un origen de datos para Windows  
  
1.  Abra el Administrador de orígenes de datos ODBC.  
  
2.  En el cuadro de diálogo Administrador de orígenes de datos ODBC, haga clic en Agregar. Aparece el cuadro de diálogo Crear nuevo origen de datos.  
  
3.  Seleccione Microsoft ODBC para Oracle y, a continuación, haga clic en Finalizar. Aparece el ODBC de Microsoft para el cuadro de diálogo de configuración de Oracle.  
  
4.  En el cuadro Nombre de origen de datos, escriba el nombre del origen de datos que desea tener acceso. Puede ser cualquier nombre que elija.  
  
5.  En el cuadro Descripción, escriba la descripción para el controlador. Este campo opcional describe el controlador de base de datos que se conecta el origen de datos. Puede ser cualquier nombre que elija.  
  
6.  En el cuadro Nombre de usuario, escriba el nombre de usuario de base de datos (el identificador de usuario de base de datos).  
  
7.  En el cuadro servidor, escriba el Alias de la base de datos o cadena para el motor de servidor de Oracle que desea tener acceso de conexión.  
  
8.  Haga clic en Aceptar para agregar este origen de datos.  
  
> [!NOTE]  
>  Aparece el cuadro de diálogo orígenes de datos y el Administrador de ODBC se actualiza la información del registro. El usuario asigne un nombre y la cadena que ha escrito de conexión se convierten en los valores de conexión predeterminados para este origen de datos cuando se conecta a él.  
  
1.  Haga clic en establecer de las opciones más especificaciones sobre el controlador ODBC para la instalación de Oracle:  
  
    -   **Traducción** , haga clic en Seleccionar para elegir un convertidor de datos cargado. El valor predeterminado es \<ningún convertidor >.  
  
    -   **Rendimiento** : los comentarios de incluir en la casilla de verificación de las funciones de catálogo especifica si el controlador devuelve columnas de la sección Comentarios para el [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) conjunto de resultados. El controlador ODBC para Oracle proporciona un acceso más rápido cuando no se establece este valor.  
  
         Los SINÓNIMOS de incluir en la casilla de verificación de las columnas SQL especifica si el controlador devuelve información de columna. **Tamaño del búfer** especifica el tamaño, en bytes, asignada para recibir los datos capturados. El controlador optimiza la recuperación para que una búsqueda desde el servidor Oracle devuelve las filas suficientes para rellenar un búfer del tamaño especificado. Los valores más grandes tienden a aumentar el rendimiento al recuperar una gran cantidad de datos.  
  
    -   **Personalización** : casilla el exigir ODBC DayOfWeek estándar especifica si el conjunto de resultados se ajustará al formato de día de la semana especificado de ODBC (el domingo = 1; El sábado = 7). Si esta casilla está desactivada, se devuelve el valor de Oracle específica de la configuración regional.  
  
         El SQLDescribeCol **siempre devuelve un valor de precisión** casilla especifica si el controlador debe devolver un valor distinto de cero para el *cbColDef* argumento de **SQLDescribeCol**. Este atributo de cadena de conexión solo se aplica a las columnas donde no hay ninguna escala definida en Oracle, como calcular numéricas columnas y las columnas definidas como número sin una precisión o escala. Un **SQLDescribeCol** llamada devuelve 130 para la precisión cuando Oracle no proporciona esa información. Si esta casilla está desactivada, el controlador devolverá 0 para estos tipos de columnas.  
  
2.  Haga clic en Agregar para agregar otro origen de datos, o haga clic en Cerrar para salir.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Para modificar un origen de datos de Windows  
  
1.  Abra el Administrador de orígenes de datos ODBC. Haga clic en la ficha DSN correspondiente.  
  
2.  Seleccione el origen de datos de Oracle que desea modificar y, a continuación, haga clic en configurar. Aparece el ODBC de Microsoft para el cuadro de diálogo de configuración de Oracle.  
  
3.  Modificar los campos de origen de datos aplicable y, a continuación, haga clic en Aceptar.  
  
 Cuando haya terminado de modificar la información de este cuadro de diálogo, el Administrador de ODBC actualiza la información del registro.
