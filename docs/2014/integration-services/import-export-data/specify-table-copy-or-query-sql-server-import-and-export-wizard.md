---
title: Especificar copia de tabla o consulta (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 524e878933652699bef6e31da42d3a784b54df7c
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58394423"
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>Especificar copia de tabla o consulta (Asistente para importación y exportación de SQL Server)
  Use la **especificar copia de tabla o consulta** página para especificar cómo copiar datos. Puede utilizar una interfaz gráfica para seleccionar los objetos de la base de datos existentes que desea copiar, o bien, puede utilizar Transact-SQL para crear una consulta más compleja.  
  
 Para obtener más información acerca de este asistente, vea [Asistente para importación y exportación de SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información acerca de las opciones para iniciar el asistente, así como los permisos necesarios para ejecutar el asistente correctamente, consulte [ejecutar la importación de SQL Server y el Asistente para exportación de](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de SQL Server es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opciones  
 **Copiar los datos de una o varias tablas o vistas**  
 Copiar los campos de vistas y tablas de origen seleccionado para el destino o destinos especificados mediante el **seleccionar tablas de origen y las vistas** cuadro de diálogo. Utilice esta opción si desea copiar todos los datos en el origen sin tener que filtrar ni ordenar registros.  
  
 Al utilizar un proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para conectar con un origen de datos, la opción **Copiar los datos de una o varias tablas o vistas** podría no estar disponible. Esta opción solo está disponible para los proveedores que tienen una sección ProviderDescription en el archivo ProviderDescriptors.xml. Cada sección ProviderDescription contiene la información que se necesita para recuperar los metadatos del proveedor correspondiente. De forma predeterminada, el archivo ProviderDescriptors.xml contiene una sección ProviderDescription para solo los proveedores siguientes:  
  
-   System.Data.SqlClient  
  
-   System.Data.OracleClient  
  
-   System.Data.OleDb  
  
-   System.Data.Odbc  
  
 Para realizar la **copiar datos de una o varias tablas o vistas** opción disponible para los proveedores adicionales, otros fabricantes pueden agregar sus propias secciones ProviderDescriptor al archivo ProviderDescriptors.xml. De forma predeterminada, este archivo está en \< *unidad*>: \Program Files\Microsoft SQL Server\100\DTS\ProviderDescriptors. Para revisar los requisitos de la sección ProviderDescriptor, vea el archivo de esquema ProviderDescriptors.xsd que está, de forma predeterminada, en la misma carpeta que el archivo ProviderDescriptors.xml.  
  
 **Escribir una consulta para especificar los datos que se van a transferir**  
 Genere instrucciones SQL para recuperar filas mediante la **proporcionar una consulta de origen** cuadro de diálogo. Utilice esta opción si desea modificar o restringir los datos de origen durante la operación de copia. Solo están disponibles para copiarse las filas que coincidan con los criterios de selección.  
  
  
