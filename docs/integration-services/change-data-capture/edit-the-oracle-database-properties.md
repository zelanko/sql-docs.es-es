---
title: Editar las propiedades de la base de datos de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraProp
ms.assetid: 58dc99f1-ee6b-4508-bb66-2bc589611ff7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e9178a16bf828d585e5f9fd3ae74a905fa6a0428
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71298773"
---
# <a name="edit-the-oracle-database-properties"></a>Editar las propiedades de la base de datos de Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use la pestaña Oracle del editor de propiedades para realizar cambios en la descripción que proporcionó en la página Crear base de datos CDC del Asistente para nueva instancia y para realizar cambios en la información de conexión a bases de datos de minería de registros de Oracle.  
  
 A continuación se describe la información de la pestaña **Oracle** .  
  
 **Nombre**  
 Nombre de la instancia CDC que especificó en la página Crear base de datos CDC del Asistente para nueva instancia. Este campo es de solo lectura y no puede editar esta información.  
  
 **Descripción**  
 Puede editar la descripción de la nueva instancia o agregar una si no lo hizo al crear la instancia CDC.  
  
 **Cadena de conexión de Oracle**  
 Cadena de conexión de Oracle al equipo que tiene la base de datos de Oracle que está usando. Este campo es de solo lectura y no puede editar esta información. Esto se debe a que algunos cambios en la cadena de conexión pueden hacer que la instancia CDC de Oracle apunte a otra base de datos de Oracle, lo que dañaría el estado de la instancia CDC almacenada en la tabla **cdc.xdbcdc_config** . Si es necesario realizar pequeños cambios, puede cambiar la cadena de conexión directamente en la tabla de configuración mediante SQL Server Management Studio.  
  
 **Autenticación de minería de registros de Oracle**  
 Para especificar las credenciales de autenticación de la base de datos de Oracle que contiene el extractor de registros, seleccione una de las opciones siguientes en **Autenticación**:  
  
-   **Autenticación de Windows**: seleccione esta opción para usar las credenciales del dominio de Windows actual. Solo puede usar esta opción si la base de datos de Oracle está configurada para usar la autenticación de Windows.  
  
-   **Autenticación de Oracle**: si selecciona esta opción, debe escribir el **Nombre de usuario** y la **Contraseña** para el usuario en la base de datos de Oracle a la que se está conectando.  
  
 Puede ver las propiedades de la base de datos de Oracle en el visor. Cuando se usa el visor, la información es de solo lectura. El visor también incluye una lista de las columnas capturadas de la tabla. Para obtener información acerca de cómo obtener acceso al visor, vea [How to Manage a CDC Instance](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md).  
  
## <a name="see-also"></a>Consulte también  
 [Cómo administrar un servicio CDC desde la Consola del diseñador CDC](../../integration-services/change-data-capture/how-to-manage-a-cdc-service-from-the-cdc-designer-console.md)   
 [Conectarse a una base de datos de origen de Oracle](../../integration-services/change-data-capture/connect-to-an-oracle-source-database.md)   
 [Conectar con Oracle](../../integration-services/change-data-capture/connect-to-oracle.md)  
  
  
