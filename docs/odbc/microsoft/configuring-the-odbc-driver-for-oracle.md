---
title: Configuración del controlador ODBC para Oracle ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bbdbe36ed9e6f254e2b738479698bd9eece09f8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281375"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>Configurar el controlador ODBC para Oracle
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Puede controlar el rendimiento del controlador ODBC para Oracle conociendo el entorno de datos y estableciendo correctamente los parámetros de la conexión del origen de datos a través del cuadro de diálogo Administrador de [orígenes](../../odbc/admin/odbc-data-source-administrator.md) de datos ODBC o mediante los parámetros de cadena de conexión. El cuadro de diálogo proporciona los siguientes controles para conectarse a un origen de datos mediante el cuadro de diálogo o mediante cadenas de conexión:  
  
-   **Ficha DSN de** usuario Enumera los nombres de origen de datos que son locales para el equipo.  
  
-   **Ficha DSN del sistema** Permite agregar o quitar un origen de datos del sistema. Todos los usuarios del equipo local pueden acceder a los orígenes de datos del sistema.  
  
-   **Ficha DSN de** archivo Permite agregar o quitar un origen de datos de archivo del equipo local. Los orígenes de datos de archivo pueden ser compartidos por todos los usuarios que tengan el mismo controlador instalado.  
  
-   **Pestaña Controladores** Enumera los controladores ODBC instalados.  
  
-   **Pestaña Seguimiento** Permite especificar cómo el Administrador de controladores ODBC realiza un seguimiento de las llamadas a funciones ODBC. Puede configurar el seguimiento por separado para cada aplicación ODBC instalada.  
  
-   **Pestaña Agrupación de conexiones** Permite seleccionar opciones de conexión para cada controlador instalado.  
  
-   **Acerca de la pestaña** Enumera los archivos de componentes ODBC instalados.  
  
 Después de agregar un origen de datos, puede usar el cuadro de diálogo Administrador de **orígenes** de datos ODBC para configurar el acceso al origen de datos. Seleccione un origen de datos y, a continuación, haga clic en una de las pestañas para editar o revisar la información.
