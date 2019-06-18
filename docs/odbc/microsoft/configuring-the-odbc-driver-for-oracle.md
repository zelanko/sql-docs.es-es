---
title: Configurar el controlador ODBC para Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- configuring ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], configuring
ms.assetid: 0a5f827c-0b80-4627-85cb-f10292b9fb33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae444cfb293e12bd94281957335da1d4f4a97885
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63301746"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>Configurar el controlador ODBC para Oracle
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 Puede controlar el rendimiento del controlador ODBC para Oracle conociendo el entorno de datos y configurar correctamente los parámetros de la conexión de origen de datos a través de la [Administrador de orígenes de datos ODBC](../../odbc/admin/odbc-data-source-administrator.md) diálogo cuadro, o a través de connect parámetros de cadena. El cuadro de diálogo proporciona los siguientes controles para conectarse a un origen de datos mediante el cuadro de diálogo o el uso de cadenas de conexión:  
  
-   **Ficha DSN de usuario** muestra los nombres de origen de datos que están en el equipo local.  
  
-   **Ficha DSN de sistema** permite agregar o quitar un origen de datos del sistema. Orígenes de datos del sistema pueden tener acceso a todos los usuarios en el equipo local.  
  
-   **Ficha DSN de archivo** permite agregar o quitar un origen de datos de archivo desde el equipo local. Orígenes de datos de archivo se pueden compartir por todos los usuarios que tienen el mismo controlador instalado.  
  
-   **Ficha controladores** se enumeran los controladores ODBC instalados.  
  
-   **Ficha seguimiento** le permite especificar cómo el Administrador de controladores ODBC realiza un seguimiento de las llamadas a funciones ODBC. Puede configurar el seguimiento por separado para cada aplicación de ODBC instalado.  
  
-   **Pestaña de agrupación de conexiones** le permite seleccionar las opciones de conexión para cada controlador instalado.  
  
-   **Acerca de la ficha** enumera los archivos de componentes ODBC instalados.  
  
 Después de agregar un origen de datos, puede usar el **Administrador de orígenes de datos ODBC** cuadro de diálogo para configurar el acceso al origen de datos. Seleccione un origen de datos y, a continuación, haga clic en una de las pestañas para modificar o revisar la información.
