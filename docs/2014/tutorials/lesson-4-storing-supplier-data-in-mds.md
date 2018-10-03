---
title: 'Lección 4: Almacenar datos de proveedor en MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: bacd9eaf-4d12-4f25-aec7-d785dec1b623
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 363b92c975bd80f4d3298a2082b6cedfee9b1263
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048826"
---
# <a name="lesson-4-storing-supplier-data-in-mds"></a>Lección 4: almacenar datos de proveedor en MDS
  Master Data Services (MDS) es la solución de SQL Server para la administración de datos maestros. La administración de datos maestros (MDM) describe los esfuerzos realizados por una organización para detectar y definir listas no transaccionales de datos.  
  
 Los modelos son el nivel superior de la organización de Master Data Services y organizan la estructura de los datos maestros. La implementación de MDS puede tener uno o varios modelos, donde cada modelo agrupa datos similares. En general, los datos maestros se pueden clasificar en una de estas cuatro categorías: personas, lugares, cosas o conceptos. Por ejemplo, puede crear un modelo Producto que vaya a contener datos relacionados con productos o un modelo Cliente para que contenga datos relacionados con clientes. Vea [Modelos (Master Data Services)](http://msdn.microsoft.com/library/ee633746.aspx) para obtener más detalles.  
  
 Un modelo puede contener una o varias entidades. Cada entidad tiene atributos (columnas) y miembros (filas). Cada fila contiene los datos maestros. En esta lección, creará un modelo Proveedores con dos entidades denominadas Proveedor y Estado. La entidad Proveedor tendrá los atributos siguientes: Código, Nombre, Nombre de contacto, Apellido de contacto, Dirección de correo electrónico de contacto, Línea de dirección, Ciudad, Estado, Código postal y País. Vea [Atributos (Master Data Services)](http://msdn.microsoft.com/library/ee633745.aspx) para obtener más detalles sobre los atributos en general. Los atributos Código y Nombre corresponden a las columnas SupplierID y Supplier Name del archivo de Excel Cleansed and Matched Suppliers.  
  
 Un atributo basado en dominio es un atributo con valores rellenados por miembros de otra entidad. Los atributos basados en dominio impiden que los usuarios escriban valores de atributo que no sean válidos. Un valor de atributo solo se puede seleccionar en la lista desplegable rellena por otra entidad. En este tutorial, el atributo Estado de la entidad Proveedor es un atributo basado en dominio con valores de la entidad Estado. Solo puede cambiar el valor del atributo Estado de la entidad Proveedor a uno de los valores de la entidad Estado. Vea [Atributos basados en dominio](../master-data-services/domain-based-attributes-master-data-services.md) para obtener más detalles.  
  
 En MDS, una jerarquía derivada se deriva de la relación de atributo basado en dominio del modelo. En este tutorial, creará una jerarquía derivada entre las entidades Proveedor y Estado. Después de crear la jerarquía derivada, verá una lista de estados en el explorador de Master Data Manager. Al hacer clic en un estado en la lista, verá los proveedores de ese estado en el panel derecho. Más adelante creará una jerarquía derivada basada en esta relación. Vea [Jerarquías derivadas](../master-data-services/derived-hierarchies-master-data-services.md) para obtener más detalles.  
  
 Ha creado una base de conocimiento en DQS y la ha usado para limpiar y buscar coincidencias en los datos de proveedor, y ha almacenado los resultados en el archivo Cleansed and Matched Supplier Data.xls. En esta lección, cargará los datos limpios y coincidentes en MDS. DQS solo contiene información sobre los datos (metadatos), mientras que MDS almacena los datos propiamente dichos (conjunto maestro). Por ejemplo: DQS puede tener información sobre varios proveedores, pero MDS solo mantiene los proveedores que una empresa usa.  
  
 En esta lección, realizará las tareas siguientes:  
  
1.  Crear el modelo **Proveedores** en **MDS** mediante la **aplicación web de Master Data Manager**.  
  
2.  Abrir **Cleansed and Matched Supplier Data.xls** en Excel y usar el **complemento MDS para Excel** para crear una entidad denominada **Proveedor** y cargar los datos en MDS.  
  
3.  Comprobar que los datos se crean en MDS mediante **Master Data Manager**.  
  
4.  Crear una entidad denominada **Estado** y actualizar el atributo **Estado** de la entidad **Proveedor** para que sea un atributo basado en dominio según la entidad **Estado** . Todo esto se hace con el **complemento MDS para Excel**.  
  
5.  Comprobar que el atributo basado en dominio se crea mediante **Master Data Manager** y actualizar los valores del atributo **Nombre** de la entidad **Estado** .  
  
6.  Ver las actualizaciones que realizó con **Master Data Manager** en **Excel**.  
  
7.  Cargar valores de la entidad **Estado** en **Excel** y agregar un valor, y comprobar que se ha agregado con **Master Data Manager**.  
  
8.  Crear y usar una jerarquía derivada mediante la relación de atributo basado en dominio entre las entidades **Proveedor** y **Estado** (el atributo Estado de la entidad Proveedor es de tipo entidad Estado) mediante **Master Data Manager**.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 1: Crear el modelo Proveedores mediante Master Data Manager](../../2014/tutorials/task-1-creating-suppliers-model-using-master-data-manager.md)  
  
  
