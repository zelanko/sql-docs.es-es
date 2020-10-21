---
title: Propiedades de la base de datos (página ChangeTracking) | Microsoft Docs
description: Obtenga información sobre cómo usar la pestaña ChangeTracking en el cuadro de diálogo Propiedades de la base de datos para ver o modificar la configuración del seguimiento de cambios de una base de datos.
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.changetracking.f1
ms.assetid: 9b929640-bc62-449b-9b06-b5a77b8cf372
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7129094815add7f3f49aaa5e99b353b3f656a848
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193026"
---
# <a name="database-properties-changetracking-page"></a>Propiedades de la base de datos (página ChangeTracking)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Utilice esta página para ver o modificar la configuración del seguimiento de cambios de la base de datos seleccionada. Para obtener más información sobre las opciones disponibles en esta página, vea [Habilitar y deshabilitar el seguimiento de cambios &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md).  
  
## <a name="options"></a>Opciones  
 **Seguimiento de cambios**  
 Utilice esta opción para habilitar o deshabilitar el seguimiento de cambios de la base de datos.  
  
 Para habilitar el seguimiento de cambios, debe tener el permiso para modificar la base de datos.  
  
 Al cambiar el valor a **True** , se establece una opción de base de datos que permite habilitar el seguimiento en tablas individuales.  
  
 También puede configurar el seguimiento de cambios utilizando [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md).  
  
 **Período de retención**  
 Especifica el período mínimo para mantener la información de seguimiento de cambios en la base de datos. Los datos se quitarán solo si el valor **Auto Clean-Up** es **True**.  
  
 El valor predeterminado es 2.  
  
 **Unidades del período de retención**  
 Especifica las unidades para el valor del Período de retención. Puede seleccionar **Días**, **Horas**o **Minutos**. El valor predeterminado es **Días**.  
  
 El período de retención mínimo es de 1 minuto. No hay ningún período de retención máximo.  
  
 **Limpieza automática**  
 Indica si los datos del seguimiento de cambios se quitan automáticamente después del período de retención especificado.  
  
 Al habilitar la opción **Limpieza automática** , se restablece cualquier período de retención anterior personalizado al valor predeterminado de 2 días.  
  
## <a name="see-also"></a>Consulte también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-transact-sql.md)  
  
