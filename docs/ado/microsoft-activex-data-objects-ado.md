---
title: Microsoft ActiveX Data Objects (ADO) | Documentos de Microsoft
ms.custom: 
ms.date: 07/25/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 28fa2c279cfd7964d8516514a3caed129e335692
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX Data Objects (ADO)

En programas de C++, se utiliza ADO para conectarse a SQL Server. Por supuesto, también funciona para conectarse a la base de datos de SQL de Azure en la nube.

Cada sección de este artículo describe un componente de ADO.

> [!NOTE]
> ADO.NET es diferente de ADO. ADO.NET y muchos otros controladores de conexión de SQL y sus idiomas, se analizan a partir de [controladores de SQL Server](../connect/sql-connection-libraries.md).

  
## <a name="ado"></a>ADO  
 Microsoft ActiveX Data Objects (ADO) permiten a las aplicaciones cliente tener acceso y manipular los datos desde una variedad de orígenes a través de un proveedor OLE DB. Sus principales ventajas son la facilidad de uso, alta velocidad, baja sobrecarga de memoria y un poco espacio en disco. ADO admite características clave para la creación de aplicaciones basadas en Web y cliente/servidor.  
  
## <a name="ado-md"></a>ADO MD  
 Microsoft ActiveX Data Objects (Multidimensional) (ADO MD) proporciona un acceso sencillo a datos multidimensionales de lenguajes como Microsoft Visual Basic y Microsoft Visual C++. ADO MD amplía Microsoft ActiveX Data Objects (ADO) para que incluya objetos específicos de datos multidimensionales, como los objetos CubeDef y Cellset. Con ADO MD puede explorar un esquema multidimensional, consultar un cubo y recuperar los resultados.  
  
 Al igual que ADO, ADO MD utiliza un proveedor OLE DB subyacente para obtener acceso a datos. Para trabajar con ADO MD, el proveedor debe ser un proveedor de datos multidimensionales (MDP) de acuerdo con la especificación OLE DB para OLAP. Proveedores de datos multidimensionales presentan datos en vistas multidimensionales, en lugar de proveedores de datos tabulares (TDP) que presentan los datos en vistas tabulares. Consulte la documentación para el proveedor OLE DB de OLAP para obtener más información sobre la sintaxis específica y comportamientos admitidos por el proveedor.  
  
## <a name="rds"></a>RDS  
 Servicio de datos remoto (RDS) es una característica de ADO, con la que puede mover datos desde un servidor a una aplicación cliente o una página Web, manipular los datos en el cliente y devolver actualizaciones al servidor en un viaje de ida y.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="adox"></a>ADOX  
 Microsoft ActiveX Data Objects Extensions for Data Definition Language and Security (ADOX) es una extensión de los objetos de ADO y el modelo de programación. ADOX incluye objetos de esquema, creación y modificación, así como de seguridad. Dado que es un enfoque basado en objetos para la manipulación de esquema, puede escribir código que funcionará con datos de diversos orígenes independientemente de las diferencias de sus sintaxis nativas.  
  
 ADOX es una biblioteca complementaria a los objetos ADO básicos. Expone objetos adicionales para crear, modificar y eliminar objetos del esquema, como tablas y procedimientos. También incluye objetos de seguridad para mantener a los usuarios y grupos y para conceder y revocar permisos en objetos.  
  
## <a name="documentation"></a>Documentación  
 [Problemas de diseño de seguridad de ADO](../ado/guide/ado-security-design-issues.md)  
  
 [Guía del programador de ADO](../ado/guide/ado-programmer-s-guide.md)  
  
 Introducción al uso de ADO, RDS, ADO MD y ADOX.  
  
 [Referencia del programador de ADO](../ado/reference/ado-programmer-s-reference.md)  
  
 Esta sección de la documentación de ADO contiene temas para cada ADO, RDS, ADO MD y ADOX objeto, colección, propiedad, propiedad dinámica, método, evento y enumeración.  
  
 [Glosario de ADO](../ado/ado-glossary.md)  
  
## <a name="support"></a>Soporte técnico  
 De forma gratuita ayuda con problemas de ADO, pruebe a publicar en el grupo de noticias público de ADO. Este grupo de noticias se supervisa por profesionales de soporte técnico de servicios de soporte de producto de Microsoft (PSS) que cubren ADO y por otros desarrolladores experimentados de ADO.  
  
 Encontrará más información sobre opciones de soporte técnico en el sitio Web de soporte técnico y de Microsoft Help.



