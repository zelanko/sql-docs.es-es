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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bbdbe36ed9e6f254e2b738479698bd9eece09f8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281375"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>Configurar el controlador ODBC para Oracle
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Puede controlar el rendimiento del controlador ODBC para Oracle conociendo el entorno de datos y estableciendo correctamente los parámetros de la conexión del origen de datos a través del cuadro de diálogo [Administrador de orígenes de datos ODBC](../../odbc/admin/odbc-data-source-administrator.md) o a través de los parámetros de cadena de conexión. El cuadro de diálogo proporciona los siguientes controles para conectarse a un origen de datos mediante el cuadro de diálogo o mediante cadenas de conexión:  
  
-   **Pestaña DSN de usuario** Enumera los nombres de los orígenes de datos que son locales para el equipo.  
  
-   **Ficha DSN de sistema** Permite agregar o quitar un origen de datos del sistema. Todos los usuarios del equipo local pueden tener acceso a los orígenes de datos del sistema.  
  
-   **Ficha DSN de archivo** Permite agregar o quitar un origen de datos de archivo del equipo local. Todos los usuarios que tienen instalado el mismo controlador pueden compartir los orígenes de datos de archivo.  
  
-   **Pestaña controladores** Enumera los controladores ODBC instalados.  
  
-   **Pestaña seguimiento** Permite especificar cómo realiza el seguimiento del administrador de controladores ODBC las llamadas a funciones ODBC. Puede configurar el seguimiento por separado para cada aplicación ODBC instalada.  
  
-   **Pestaña agrupación de conexiones** Permite seleccionar las opciones de conexión para cada controlador instalado.  
  
-   **Ficha acerca de** Enumera los archivos de componentes ODBC instalados.  
  
 Después de agregar un origen de datos, puede utilizar el cuadro de diálogo **Administrador de orígenes de datos ODBC** para configurar el acceso al origen de datos. Seleccione un origen de datos y, a continuación, haga clic en una de las pestañas para editar o revisar la información.
