---
description: Pantalla 1 del Asistente para orígenes de datos (ODBC Driver for SQL Server)
title: Pantalla del Asistente para orígenes de datos 1 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78009925b5d62e8a314d0a3fdc27c29acaee5c5d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462229"
---
# <a name="data-source-wizard-screen-1"></a>Pantalla del Asistente para orígenes de datos 1

Especifique el nombre y la descripción del origen de datos y el nombre del servidor que ejecuta SQL Server al que se conectará el origen de datos. 
    
## <a name="options"></a>Opciones

### <a name="name"></a>NOMBRE

El nombre del origen de datos usado por una aplicación ODBC cuando solicita una conexión al origen de datos. Por ejemplo, "Personal". El nombre del origen de datos se muestra en el cuadro de diálogo Administrador de orígenes de datos ODBC.

### <a name="description"></a>Descripción

(Opcional) Una descripción del origen de datos. Por ejemplo, "Fecha de contratación, historial del sueldo y la revisión actual de todos los empleados."

### <a name="select-or-enter-a-server-name"></a>Seleccionar o especificar un nombre de servidor

Nombre de una instancia de SQL Server en la red. Tendrá que especificar un servidor en el siguiente cuadro de edición.

En la mayoría de los casos, el controlador ODBC puede conectarse utilizando el orden de protocolo predeterminado y el nombre del servidor proporcionado en este cuadro. Use el Administrador de configuración de SQL Server si desea crear un alias para el servidor o configurar las bibliotecas de red de cliente.

Puede escribir "(local)" en el cuadro del servidor cuando esté utilizando el mismo equipo que SQL Server. El usuario puede establecer conexión con una instancia local de SQL Server, incluso si ejecuta una versión que no está en red de SQL Server. Pueden ejecutarse varias instancias de SQL Server en el mismo equipo. Para especificar una instancia con nombre de SQL Server, el nombre del servidor se especifica como _nombreDeServidor_\\_nombreDeInstancia_.

Para más información acerca de los nombres de servidor para diferentes tipos de redes, vea la documentación de la instalación de SQL Server en los Libros en pantalla de SQL Server.

### <a name="finish"></a>Finalizar

Si la información especificada en esta pantalla es todo lo que se necesita para conectar con SQL Server, puede hacer clic en **Finalizar**. Los valores predeterminados se utilizan para todos los atributos especificados en otras pantallas del asistente.

### <a name="next"></a>Siguientes

Para continuar con la siguiente pantalla del asistente, haga clic en **Siguiente**.

## <a name="next-steps"></a>Pasos siguientes

[Pantalla del Asistente para orígenes de datos 2](../../../connect/odbc/windows/dsn-wizard-2.md)
