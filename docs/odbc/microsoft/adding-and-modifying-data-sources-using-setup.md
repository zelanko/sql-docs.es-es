---
title: Adición y modificación de orígenes de datos mediante la instalación de la instalación de la instalación de la aplicación de la instalación de Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae76abc902e4687e5d9891871d7d5d60598b3abc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281415"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>Agregar y modificar orígenes de datos mediante el programa de instalación
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Un origen de datos identifica una ruta de acceso a los datos que puede incluir una biblioteca de red, un servidor, una base de datos y otros atributos, en este caso, el origen de datos es la ruta de acceso a una base de datos de Oracle. Para conectarse a un origen de datos, el Administrador de controladores comprueba el registro de Windows para obtener información de conexión específica.  
  
 La entrada del Registro creada por el Administrador de orígenes de datos ODBC la usan el Administrador de controladores ODBC y los controladores ODBC. Esta entrada contiene información sobre cada origen de datos y su controlador asociado. Para poder conectarse a un origen de datos, su información de conexión debe agregarse al registro.  
  
 Para agregar y configurar orígenes de datos, utilice el Administrador de [orígenes de datos ODBC](../../odbc/admin/odbc-data-source-administrator.md). El Administrador ODBC actualiza la información de conexión del origen de datos. A medida que agrega orígenes de datos, el Administrador ODBC actualiza la información del Registro automáticamente.  
  
### <a name="to-add-a-data-source-for-windows"></a>Para agregar un origen de datos para Windows  
  
1.  Abra el Administrador de orígenes de datos ODBC.  
  
2.  En el cuadro de diálogo Administrador de orígenes de datos ODBC, haga clic en Agregar. Aparece el cuadro de diálogo Creat New Data Source.  
  
3.  Seleccione Microsoft ODBC para Oracle y, a continuación, haga clic en Finalizar. Aparece el cuadro de diálogo Configuración de Microsoft ODBC para Oracle.  
  
4.  En el cuadro Nombre del origen de datos, escriba el nombre del origen de datos al que desea tener acceso. Puede ser cualquier nombre que elija.  
  
5.  En el cuadro Descripción, escriba la descripción del controlador. Este campo opcional describe el controlador de base de datos al que se conecta el origen de datos. Puede ser cualquier nombre que elija.  
  
6.  En el cuadro Nombre de usuario, escriba el nombre de usuario de la base de datos (su ID de usuario de base de datos).  
  
7.  En el cuadro Servidor, escriba el Alias de base de datos o la cadena connect para el motor de Oracle Server al que desea tener acceso.  
  
8.  Haga clic en Aceptar para agregar este origen de datos.  
  
> [!NOTE]  
>  Aparece el cuadro de diálogo Orígenes de datos y el Administrador ODBC actualiza la información del Registro. El nombre de usuario y la cadena de conexión que ha escrito se convierten en los valores de conexión predeterminados para este origen de datos cuando se conecta a él.  
  
1.  Haga clic en Opciones para hacer más especificaciones sobre la configuración del controlador ODBC para Oracle:  
  
    -   **Traducción:** haga clic en Seleccionar para elegir un traductor de datos cargado. El valor \<predeterminado es No Translator>.  
  
    -   **Rendimiento:** la casilla Incluir MARCAS en funciones de catálogo especifica si el controlador devuelve columnas Comentarios para el conjunto de resultados [SQLColumns.](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) El controlador ODBC para Oracle proporciona un acceso más rápido cuando no se establece este valor.  
  
         La casilla Incluir SYNONYMS en columnas SQL especifica si el controlador devuelve información de columna. **Tamaño del búfer** especifica el tamaño, en bytes, asignado para recibir los datos capturados. El controlador optimiza la obtención para que una captura del servidor de Oracle devuelva suficientes filas para rellenar un búfer del tamaño especificado. Los valores más grandes tienden a aumentar el rendimiento al obtener una gran cantidad de datos.  
  
    -   **Personalización:** la casilla de verificación Aplicar ODBC DayOfWeek Standard especifica si el conjunto de resultados se ajustará al formato de día de la semana especificado por ODBC (domingo 1; Sábado 7). Si esta casilla de verificación está desactivada, se devuelve el valor de Oracle específico de la configuración regional.  
  
         La casilla SQLDescribeCol **siempre devuelve un valor para la precisión** especifica si el controlador debe devolver o no un valor distinto de cero para el argumento *cbColDef* de **SQLDescribeCol**. Este atributo de cadena de conexión solo se aplica a las columnas en las que no hay ninguna escala definida por Oracle, como columnas numéricas calculadas y columnas definidas como NUMBER sin precisión ni escala. Una llamada **SQLDescribeCol** devuelve 130 para la precisión cuando Oracle no proporciona esa información. Si esta casilla de verificación está desactivada, el controlador devolverá 0 para estos tipos de columnas en su lugar.  
  
2.  Haga clic en Agregar para agregar otro origen de datos o haga clic en Cerrar para salir.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Para modificar un origen de datos para Windows  
  
1.  Abra el Administrador de orígenes de datos ODBC. Haga clic en la pestaña DSN adecuada.  
  
2.  Seleccione el origen de datos de Oracle que desea modificar y, a continuación, haga clic en Configurar. Aparece el cuadro de diálogo Configuración de Microsoft ODBC para Oracle.  
  
3.  Modifique los campos de origen de datos aplicables y, a continuación, haga clic en Aceptar.  
  
 Cuando haya terminado de modificar la información de este cuadro de diálogo, el Administrador ODBC actualiza la información del Registro.
