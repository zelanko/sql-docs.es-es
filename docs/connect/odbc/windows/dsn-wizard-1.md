---
title: Pantalla 1 (controlador ODBC para SQL Server) del Asistente del origen de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d97cbdf8e73254b790ff0c8f965fa8b6d647951a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-wizard-screen-1"></a>Pantalla 1 del Asistente de origen de datos

Especifique el nombre y la descripción del origen de datos y el nombre del servidor que ejecuta SQL Server al que se conectará el origen de datos. 
    
## <a name="options"></a>Opciones

### <a name="name"></a>Nombre

El nombre del origen de datos usado por una aplicación ODBC cuando solicita una conexión al origen de datos. Por ejemplo, "Personal". El nombre del origen de datos se muestra en el cuadro de diálogo Administrador de orígenes de datos ODBC.

### <a name="description"></a>Description

(Opcional) Una descripción del origen de datos. Por ejemplo, "Fecha de contratación, historial del sueldo y la revisión actual de todos los empleados."

### <a name="select-or-enter-a-server-name"></a>Seleccionar o especificar un nombre de servidor

El nombre de una instancia de SQL Server en la red. Tendrá que especificar un servidor en el siguiente cuadro de edición.

En la mayoría de los casos, el controlador ODBC puede conectarse mediante el orden de protocolo predeterminado y el nombre del servidor proporcionado en este cuadro. Use el Administrador de configuración de SQL Server si desea crear un alias para el servidor o configurar las bibliotecas de red de cliente.

Puede escribir "(local)" en el cuadro servidor cuando se usa el mismo equipo que SQL Server. El usuario, a continuación, puede conectarse a la instancia local de SQL Server, incluso cuando se ejecuta una versión de SQL Server no está en la red. Pueden ejecutar varias instancias de SQL Server en el mismo equipo. Para especificar una instancia con nombre de SQL Server, el nombre del servidor se especifica como _ServerName_\\_nombreDeInstancia_.

Para obtener más información acerca de los nombres de servidor para diferentes tipos de redes, consulte la documentación de instalación de SQL Server en los libros en pantalla de SQL Server.

### <a name="finish"></a>Finalizar

Si la información especificada en esta pantalla es todo lo que se necesita para conectarse a SQL Server, haga clic en **finalizar**. Los valores predeterminados se utilizan para todos los atributos especificados en otras pantallas del asistente.

### <a name="next"></a>Siguiente

Para continuar con la siguiente pantalla del asistente, haga clic en **siguiente**.

## <a name="next-steps"></a>Pasos siguientes

[Pantalla 2 del Asistente de origen de datos](../../../connect/odbc/windows/dsn-wizard-2.md)
