---
title: Agregar y modificar orígenes de datos mediante el programa de instalación | Microsoft Docs
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
ms.openlocfilehash: 621d10c3c602b2f406461a24e53b2302e45835eb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901403"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>Agregar y modificar orígenes de datos mediante el programa de instalación
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Un origen de datos identifica una ruta de acceso a los datos que pueden incluir una biblioteca de red, servidor, base de datos y otros atributos; en este caso, el origen de datos es la ruta de acceso a una base de datos de Oracle. Para conectarse a un origen de datos, el administrador de controladores comprueba el registro de Windows para obtener información de conexión específica.  
  
 El administrador de controladores ODBC y los controladores ODBC utilizan la entrada del registro creada por el administrador de orígenes de datos ODBC. Esta entrada contiene información sobre cada origen de datos y su controlador asociado. Para poder conectarse a un origen de datos, se debe agregar su información de conexión al registro.  
  
 Para agregar y configurar orígenes de datos, utilice el [Administrador de orígenes de datos ODBC](../../odbc/admin/odbc-data-source-administrator.md). El administrador de ODBC actualiza la información de conexión del origen de datos. A medida que agrega orígenes de datos, el administrador de ODBC actualiza la información del registro.  
  
### <a name="to-add-a-data-source-for-windows"></a>Para agregar un origen de datos para Windows  
  
1.  Abra el administrador de orígenes de datos ODBC.  
  
2.  En el cuadro de diálogo Administrador de orígenes de datos ODBC, haga clic en Agregar. Aparecerá el cuadro de diálogo Crear nuevo origen de datos.  
  
3.  Seleccione Microsoft ODBC para Oracle y, a continuación, haga clic en finalizar. Aparece el cuadro de diálogo instalación de Microsoft ODBC para Oracle.  
  
4.  En el cuadro Nombre del origen de datos, escriba el nombre del origen de datos al que desea obtener acceso. Puede ser cualquier nombre que elija.  
  
5.  En el cuadro Descripción, escriba la descripción del controlador. Este campo opcional describe el controlador de base de datos al que se conecta el origen de datos. Puede ser cualquier nombre que elija.  
  
6.  En el cuadro Nombre de usuario, escriba el nombre de usuario de la base de datos (el ID. de usuario de base de datos).  
  
7.  En el cuadro servidor, escriba el alias de la base de datos o la cadena de conexión del motor de servidor de Oracle al que desea obtener acceso.  
  
8.  Haga clic en Aceptar para agregar este origen de datos.  
  
> [!NOTE]  
>  Aparece el cuadro de diálogo orígenes de datos y el administrador de ODBC actualiza la información del registro. El nombre de usuario y la cadena de conexión que escribió se convierten en los valores de conexión predeterminados para este origen de datos cuando se conecta a él.  
  
1.  Haga clic en opciones para obtener más especificaciones sobre la instalación del controlador ODBC para Oracle:  
  
    -   **Traducción** : haga clic en seleccionar para elegir un traductor de datos cargado. El valor predeterminado \<es sin traductor>.  
  
    -   **Rendimiento** : la casilla incluir comentarios en las funciones de catálogo especifica si el controlador devuelve columnas de comentarios para el conjunto de resultados [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) . El controlador ODBC para Oracle proporciona un acceso más rápido cuando no se establece este valor.  
  
         La casilla incluir sinónimos en columnas SQL especifica si el controlador devuelve información de columna. **Tamaño de búfer** especifica el tamaño, en bytes, que se asigna para recibir datos capturados. El controlador optimiza la captura para que una captura del servidor de Oracle devuelva suficientes filas para llenar un búfer del tamaño especificado. Los valores más grandes tienden a aumentar el rendimiento al capturar una gran cantidad de datos.  
  
    -   **Personalización** : la casilla de verificación exigir ODBC DayOfWeek Standard especifica si el conjunto de resultados se ajustará al formato de día de la semana especificado de ODBC (Sunday = 1; Sábado = 7). Si esta casilla está desactivada, se devuelve el valor de Oracle específico de la configuración regional.  
  
         La casilla SQLDescribeCol **siempre devuelve un valor para precisión** especifica si el controlador debe devolver o no un valor distinto de cero para el argumento *cbColDef* de **SQLDescribeCol**. Este atributo de cadena de conexión solo se aplica a las columnas en las que no hay ninguna escala definida por Oracle, como columnas numéricas calculadas y columnas definidas como número sin una precisión o escala. Una llamada a **SQLDescribeCol** devuelve 130 para la precisión cuando Oracle no proporciona esa información. Si esta casilla está desactivada, el controlador devolverá 0 para estos tipos de columnas.  
  
2.  Haga clic en Agregar para agregar otro origen de datos o haga clic en cerrar para salir.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Para modificar un origen de datos para Windows  
  
1.  Abra el administrador de orígenes de datos ODBC. Haga clic en la pestaña DSN adecuada.  
  
2.  Seleccione el origen de datos de Oracle que desea modificar y, a continuación, haga clic en configurar. Aparece el cuadro de diálogo instalación de Microsoft ODBC para Oracle.  
  
3.  Modifique los campos de origen de datos aplicables y, a continuación, haga clic en Aceptar.  
  
 Cuando haya terminado de modificar la información de este cuadro de diálogo, el administrador de ODBC actualizará la información del registro.
