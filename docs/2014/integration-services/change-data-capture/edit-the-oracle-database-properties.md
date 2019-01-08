---
title: Editar las propiedades de la base de datos de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraProp
ms.assetid: 58dc99f1-ee6b-4508-bb66-2bc589611ff7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cfc119c031f0eeb84317cd1bcd8250f8ab803b6b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52770867"
---
# <a name="edit-the-oracle-database-properties"></a>Editar las propiedades de la base de datos de Oracle
  Use la pestaña Oracle del editor de propiedades para realizar cambios en la descripción que proporcionó en la página Crear base de datos CDC del Asistente para nueva instancia y para realizar cambios en la información de conexión a bases de datos de minería de registros de Oracle.  
  
 A continuación se describe la información de la pestaña **Oracle** .  
  
 **Name**  
 Nombre de la instancia CDC que especificó en la página Crear base de datos CDC del Asistente para nueva instancia. Este campo es de solo lectura y no puede editar esta información.  
  
 **Descripción**  
 Puede editar la descripción de la nueva instancia o agregar una si no lo hizo al crear la instancia CDC.  
  
 **Cadena de conexión de Oracle**  
 Cadena de conexión de Oracle al equipo que tiene la base de datos de Oracle que está usando. Este campo es de solo lectura y no puede editar esta información. Esto se debe a que algunos cambios en la cadena de conexión pueden hacer que la instancia CDC de Oracle apunte a otra base de datos de Oracle, lo que dañaría el estado de la instancia CDC almacenada en la tabla **cdc.xdbcdc_config** . Si es necesario realizar pequeños cambios, puede cambiar la cadena de conexión directamente en la tabla de configuración mediante SQL Server Management Studio.  
  
 **Autenticación de minería de registros de Oracle**  
 Para especificar las credenciales de autenticación de la base de datos de Oracle que contiene el extractor de registros, seleccione una de las opciones siguientes en **Autenticación**:  
  
-   **Autenticación de Windows**: Seleccione esta opción para usar las credenciales de dominio de Windows actuales. Solo puede usar esta opción si la base de datos de Oracle está configurada para usar la autenticación de Windows.  
  
-   **Autenticación de Oracle**: Si selecciona esta opción, debe escribir el **nombre de usuario** y **contraseña** para el usuario se conecta a la base de datos de Oracle.  
  
 Puede ver las propiedades de la base de datos de Oracle en el visor. Cuando se usa el visor, la información es de solo lectura. El visor también incluye una lista de las columnas capturadas de la tabla. Para obtener información acerca de cómo obtener acceso al visor, vea [How to Manage a CDC Instance](manage-a-cdc-instance.md).  
  
## <a name="see-also"></a>Vea también  
 [Cómo administrar un servicio CDC desde la Consola del diseñador CDC](how-to-manage-a-cdc-service-from-the-cdc-designer-console.md)   
 [Conectar con una base de datos de origen de Oracle](connect-to-an-oracle-source-database.md)   
 [Conectar con Oracle](connect-to-oracle.md)  
  
  
