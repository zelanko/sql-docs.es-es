---
title: Usar ADO con lenguajes de Scripting | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scripting languages [ADO]
- ADO, scripting languages
ms.assetid: 76fc4d00-0c9f-422b-af5c-af6ed8fb29d8
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 070cfacfad680fbf0664ad5dc6bc3a01aed99520
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-ado-with-scripting-languages"></a>Usar ADO con lenguajes de Scripting
Dentro de un entorno de scripting, ADO permite exponer datos mediante secuencias de comandos de servidor. En este escenario, ADO, el proveedor OLE DB subyacente que utiliza y cualquier otro componente necesario para hacer referencia a un almacén de datos determinado está instalado en un servidor que ejecuta Internet Information Services (IIS). Utilizando páginas Active Server (ASP), ADO es un componente al que hace referencia en una secuencia de comandos que puede generar código HTML, por ejemplo. Este contenido HTML se puede pasar a través de HTTP en un explorador Web del cliente. Mediante el uso de secuencias de comandos, la página Web puede enviar acciones a la secuencia de comandos de servidor, lo que le permite actualizar, recorrer o ver datos específicos.  
  
 Antes de usar un objeto de ActiveX en una página Web, es importante saber si el objeto es seguro para scripting. Cuando un objeto se considera seguro para scripting, significa que el control no puede realizar ninguna acción perjudicial en el equipo del usuario y por lo tanto, se puede ejecutar sin solicitar la aprobación del usuario. En la tabla siguiente se enumera los objetos ADO e indica si son seguros para scripting.  
  
|Object|¿Es seguro para Scripting?|  
|------------|-------------------------|  
|Conexión ADO|Sí|  
|Comando de ADO|no|  
|Parámetro de ADO|no|  
|Conjunto de registros ADO|Sí|  
|Registro de ADO|Sí|  
|Secuencia de ADO|Sí|  
|Error de ADO.|no|  
|Catálogo ADOX|no|  
|Conjunto de celdas ADOX|no|  
|DataControl RDS|Sí|  
|DataSpace RDS|Sí|  
|DataFactory RDS|no|  
  
 En la tabla siguiente enumera los proveedores incluidos con Windows DAC/MDAC e indica si son seguros para scripting.  
  
|Proveedor|¿Es seguro para Scripting?|  
|--------------|-------------------------|  
|Forma|Sí|  
|Persist|Sí|  
|Remote|Sí|  
|Proveedor OLE DB para SQL Server (SQLOLEDB)|no|  
|Proveedor OLE DB para ODBC (MSDASQL)|no|  
  
## <a name="odbc-data-sources"></a>Orígenes de datos ODBC  
 Una diferencia importante entre el código de ADO de secuencias de comandos y secuencias de comandos no es el origen de datos ODBC, si se utiliza. Para las aplicaciones no son secuencias de comandos, puede crear un DSN de usuario en el Administrador de orígenes de datos de ODBC. Para los scripts que se ejecutan en IIS, debe crear un DSN de sistema; en caso contrario, las secuencias de comandos no reconocerán el origen de datos que creó. Esto se aplica a cualquier aplicación de secuencias de comandos de ADO mediante el proveedor Microsoft OLE DB para ODBC a través de IIS de Microsoft.  
  
## <a name="referencing-the-ado-library"></a>Hacer referencia a la biblioteca de ADO  
 No es aplicable con lenguajes de scripting.  
  
## <a name="handling-events"></a>Control de eventos  
 No es aplicable con lenguajes de scripting.  
  
 Los temas siguientes contienen información más específica sobre cómo usar ADO con lenguajes de scripting:  
  
-   [Programación ADO en VBScript](../../../ado/guide/appendixes/vbscript-ado-programming.md)  
  
-   [Programación ADO con JScript](../../../ado/guide/appendixes/jscript-ado-programming.md)  
  
## <a name="see-also"></a>Vea también  
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Usar ADO con Microsoft Visual Basic](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-basic.md)   
 [Usar ADO con Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md)   
