---
title: Regeneración de los procedimientos personalizados para los cambios de esquema (transaccional)
description: Regenere los procedimientos almacenados transaccionales personalizados para los reflejar cambios de esquema en la replicación transaccional.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- custom procedures [SQL Server replication]
- transactional replication, replicating schema changes
- schemas [SQL Server replication], replicating changes
ms.assetid: ccf68a13-e748-4455-8168-90e6d2868098
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: e20f38a055fba642795ed0c0d40d07cbff442a9b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "76287006"
---
# <a name="transactional-articles---regenerate-to-reflect-schema-changes"></a>Transactional Articles - Regenerate to Reflect Schema Changes (Artículos transaccionales: Volver a generar para reflejar cambios de esquema)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  De manera predeterminada, la replicación transaccional lleva a cabo todos los cambios de datos en los suscriptores a través de procedimientos almacenados generados por procedimientos internos para cada artículo de la tabla en la publicación. Los tres procedimientos (para inserciones, actualizaciones y eliminaciones, respectivamente) se copian al suscriptor y se ejecutan cuando se replica una inserción, actualización o eliminación en el suscriptor. Cuando se realiza un cambio de esquema en una tabla de un publicador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , la replicación vuelve a generar automáticamente estos procedimientos, llamando al mismo conjunto de procedimientos internos de scripting para que los nuevos procedimientos coincidan con el nuevo esquema (no se admite la replicación de cambios de esquema para los publicadores de Oracle).  
  
 También es posible especificar procedimientos personalizados para reemplazar uno o más de los procedimientos predeterminados. Los procedimientos personalizados se deben modificar si el cambio de esquema va a afectar al procedimiento. Por ejemplo, si un procedimiento hace referencia a una columna que se quita en un cambio de esquema, se deben quitar del procedimiento las referencias a esa columna. La replicación propaga un nuevo procedimiento personalizado a los suscriptores de dos maneras:  
  
-   La primera opción es utilizar un procedimiento de scripting personalizado para reemplazar los valores predeterminados que utiliza la replicación:  
  
    1.  Al ejecutar [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), asegúrese que el bit 0x02 de `@schema_option` está establecido en **true**.  
  
    2.  Ejecute [sp_register_custom_scripting &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md) y especifique un valor de "insert", "update" o "delete" para el parámetro `@type` y el nombre del procedimiento de scripting personalizado para el parámetro `@value`.  
  
     La siguiente vez que se lleve a cabo un cambio de esquema, la replicación llamará a este procedimiento almacenado para crear un script de la definición para el nuevo procedimiento almacenado personalizado definido por el usuario y, después, propagará el procedimiento a cada suscriptor.  
  
-   La segunda opción es utilizar un script que contenga una nueva definición de procedimiento personalizado:  
  
    1.  Al ejecutar [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), establezca el bit 0x02 de `@schema_option` en **false** para que la replicación no genere automáticamente procedimientos personalizados en el suscriptor.  
  
    2.  Antes de cada cambio de esquema, cree un nuevo archivo de script y registre el script con la replicación, ejecutando [sp_register_custom_scripting &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md). Especifique un valor de "custom_script" para el parámetro `@type` y la ruta de acceso al script en el publicador para el parámetro `@value`.  
  
     La siguiente vez que realice un cambio de esquema importante, este script se ejecutará en cada suscriptor en la misma transacción que el comando DDL. Una vez realizado el cambio de esquema, el script se elimina del registro. Debe volver a registrar el script para que se ejecute de nuevo después del siguiente cambio de esquema.  
  
## <a name="see-also"></a>Consulte también  
 [Especificar cómo se propagan los cambios para los artículos transaccionales](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)   
 [Realizar cambios de esquema en bases de datos de publicaciones](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
