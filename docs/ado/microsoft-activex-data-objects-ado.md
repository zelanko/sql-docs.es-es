---
title: Microsoft ActiveX Data Objects (ADO) | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, about
ms.assetid: 2fa6237b-44b8-4b6c-9952-5acd80a54e20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0994c4ee4c96e5ed9c373ec4bdc94b02ccddff7
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51605175"
---
# <a name="microsoft-activex-data-objects-ado"></a>Microsoft ActiveX Data Objects (ADO)

En programas de C++ se utiliza ADO para conectarse a SQL Server. Por supuesto, también funciona para conectarse a Azure SQL Database en la nube.

Cada sección en este artículo describe un componente de ADO.

> [!NOTE]
> ADO.NET es diferente de ADO. ADO.NET y muchos otros controladores de conexión de SQL y sus idiomas, se analizan a partir [controladores de SQL Server](../connect/sql-connection-libraries.md).

  
## <a name="ado"></a>ADO  
 Microsoft ActiveX Data Objects (ADO) permiten a las aplicaciones cliente tener acceso y manipular los datos desde diversos orígenes a través de un proveedor OLE DB. Sus principales ventajas son la facilidad de uso, alta velocidad, sobrecarga de memoria baja y un poco espacio en disco. ADO admite las características clave para la creación de aplicaciones basadas en Web y cliente/servidor.  
  
## <a name="ado-md"></a>ADO MD  
 Microsoft ActiveX Data Objects (Multidimensional) (ADO MD) proporciona un acceso sencillo a datos multidimensionales de lenguajes como Microsoft Visual Basic y Microsoft Visual C++. ADO MD amplía Microsoft ActiveX Data Objects (ADO) para incluir objetos específicos de datos multidimensionales, como los objetos CubeDef y Cellset. Con ADO MD puede examinar el esquema multidimensional, un cubo de consulta y recuperar los resultados.  
  
 Al igual que ADO, ADO MD usa un proveedor OLE DB subyacente para obtener acceso a datos. Para trabajar con ADO MD, el proveedor debe ser un proveedor de datos multidimensionales (MDP) tal como se define mediante la especificación OLE DB para OLAP. Proveedores de datos multidimensionales presentan datos en vistas multidimensionales en lugar de los proveedores de datos tabulares (TDP) que presentan los datos en vistas tabulares. Consulte la documentación para el proveedor OLE DB de OLAP para obtener más información sobre la sintaxis específica y comportamientos que admite el proveedor.  
  
## <a name="rds"></a>RDS  
 Servicio de datos remoto (RDS) es una característica de ADO, que puede mover datos desde un servidor a una aplicación cliente o una página Web, manipular los datos en el cliente y devolver las actualizaciones al servidor en un viaje de ida y.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="adox"></a>ADOX  
 Microsoft ActiveX Data Objects Extensions para lenguaje de definición de datos y seguridad (ADOX) es una extensión a los objetos de ADO y el modelo de programación. ADOX incluye los objetos de esquema, creación y modificación, así como de seguridad. Dado que es un enfoque basado en objetos para la manipulación de esquema, puede escribir código que funcionará con los datos de varios orígenes sin tener en cuenta las diferencias en sus sintaxis nativas.  
  
 ADOX es una biblioteca complementaria a los objetos ADO básicos. Expone objetos adicionales para crear, modificar y eliminar objetos de esquema, como tablas y procedimientos. También incluye objetos de seguridad para mantener a los usuarios y grupos y para conceder y revocar permisos en objetos.  
  
## <a name="documentation"></a>Documentación  
 [Características de diseño de seguridad de ADO](../ado/guide/ado-security-design-issues.md)  
  
 [Programador de ADO ' s guía para el uso de objetos ADO](../ado/guide/ado-programmer-s-guide.md)  
  
 Una introducción al uso de ADO, RDS, ADO MD y ADOX.  
  
 [Referencia del programador de ADO](../ado/reference/ado-programmer-s-reference.md)  
  
 Esta sección de la documentación de ADO contiene temas para cada ADO, RDS, ADO MD y ADOX objeto, colección, propiedad, propiedad dinámica, método, evento y enumeración.  
  
 [Glosario de términos de ADO](../ado/ado-glossary.md)  
  
## <a name="support"></a>Soporte técnico  
 De forma gratuita ayuda con problemas de ADO, pruebe a publicar en el grupo de noticias público de ADO. Este grupo de noticias supervisado por profesionales de soporte técnico de servicios de soporte técnico de Microsoft (PSS) que trabajan con ADO y por otros desarrolladores experimentados de ADO.  
  
 Más información acerca de las opciones de soporte técnico puede encontrarse en el sitio Web de soporte técnico y Microsoft Help.


