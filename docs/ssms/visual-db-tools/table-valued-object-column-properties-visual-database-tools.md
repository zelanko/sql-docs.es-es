---
title: Propiedades de objeto con valores de tabla (columna)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.designers.properties.QueryViewColumn
ms.assetid: 212d9bcd-aded-4313-a6b9-d7e2270e5954
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: d64ccb277d9016cd94b5613529e2d1c322162a73
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004172"
---
# <a name="table-valued-object-column-properties-visual-database-tools"></a>Propiedades (de columna) de objeto con valores de tabla (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Estas propiedades aparecen cuando selecciona una columna en un objeto de valor de tabla en el panel **Diagrama** del Diseñador de vistas y de consultas.  
  
> [!NOTE]  
> Las propiedades de este tema se ordenan por categoría en lugar de alfabéticamente.  
  
> [!NOTE]  
> Los cuadros de diálogo y comandos de menú que ve podrían diferir de aquellos que se describen en la Ayuda en función de la edición o configuración activa. Para cambiar la configuración, elija **Importar y exportar configuraciones** en el menú **Herramientas** .  
  
**Categoría Identidad**  
Se expande para mostrar la propiedad **Nombre** .  
  
**Nombre**  
Muestra el nombre de la columna seleccionada.  
  
**Categoría del Diseñador de consultas**  
Se expande para mostrar las propiedades de **Permitir valores NULL**, **Intercalación**, **Tipo de datos**, **Longitud**, **Precisión**, **Escala**y **Tamaño**.  
  
**Permitir valores NULL**  
Muestra si el tipo de datos de la columna admite o no los valores NULL.  
  
**Intercalación**  
Muestra la configuración de intercalación para la columna seleccionada. La intercalación se puede establecer en la pestaña Propiedades de columna del Diseñador de tablas.  
  
**Tipo de datos**  
Muestra el tipo de datos de la columna seleccionada.  
  
**Longitud**  
Muestra el número de caracteres o dígitos que admite el tipo de datos de la columna seleccionada. Esta propiedad solo está disponible para tipos de datos basados en caracteres.  
  
> [!NOTE]  
> Para el tamaño en bytes, consulte la propiedad **Tamaño** a continuación.  
  
**Precisión**  
Muestra el número máximo de dígitos admitido para tipos de datos numéricos. Esta propiedad muestra **0** para tipos de datos no numéricos.  
  
**Escala**  
Muestra el número máximo de dígitos que pueden aparecer a la derecha del separador decimal para los tipos de datos numéricos. Este valor debe ser menor o igual que la precisión. Esta propiedad muestra **0** para tipos de datos no numéricos.  
  
**Tamaño**  
Muestra el tamaño en bytes que admite el tipo de datos de la columna. Por ejemplo, un tipo de datos nchar puede tener una longitud de 10 (número de caracteres) pero tendría un tamaño de 20 para los juegos de caracteres Unicode.  
  
