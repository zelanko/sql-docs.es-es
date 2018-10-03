---
title: Usar ADO con lenguajes de Scripting | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- scripting languages [ADO]
- ADO, scripting languages
ms.assetid: 76fc4d00-0c9f-422b-af5c-af6ed8fb29d8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fda0fb6446609a04178b533173a82bacc34c8cb8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600393"
---
# <a name="using-ado-with-scripting-languages"></a>Usar ADO con lenguajes de Scripting
Dentro de un entorno de scripting, ADO permite exponer los datos por medio de scripting del lado servidor. En este escenario, ADO, el proveedor OLE DB subyacente que usa, y cualquier otro componente necesario para hacer referencia a un almacén de datos determinado está instalado en un servidor que ejecuta Internet Information Services (IIS). Uso de páginas Active Server (ASP), ADO es un componente al que hace referencia en una secuencia de comandos que puede generar código HTML, por ejemplo. Este contenido HTML se puede pasar a través de HTTP a un explorador Web cliente. Mediante el uso de secuencias de comandos, la página Web puede enviar acciones a la secuencia de comandos del lado servidor, lo que le permite actualizar, recorrer o ver datos específicos.  
  
 Antes de usar un objeto ActiveX en una página Web, es importante saber si el objeto es seguro para scripting. Cuando un objeto se considera seguro para scripting, significa que el control no puede realizar ninguna acción dañina en el equipo del usuario y por lo tanto, se puede ejecutar sin solicitar la aprobación del usuario. En la tabla siguiente se enumera los objetos ADO e indica si son seguros para scripting.  
  
|Objeto|¿Es seguro para Scripting?|  
|------------|-------------------------|  
|Conexión de ADO|Sí|  
|Comando de ADO|no|  
|Parámetro de ADO|no|  
|Conjunto de registros ADO|Sí|  
|Registro de ADO|Sí|  
|Stream de ADO|Sí|  
|Error de ADO.|no|  
|Catálogo ADOX|no|  
|Conjunto de celdas ADOX|no|  
|RDS DataControl|Sí|  
|DataSpace RDS|Sí|  
|RDS DataFactory|no|  
  
 En la tabla siguiente se enumera los proveedores incluidos con Windows DAC/MDAC e indica si son seguros para scripting.  
  
|Proveedor|¿Es seguro para Scripting?|  
|--------------|-------------------------|  
|Forma|Sí|  
|Persist|Sí|  
|Remote|Sí|  
|Proveedor OLE DB para SQL Server (SQLOLEDB)|no|  
|Proveedor OLE DB para ODBC (MSDASQL)|no|  
  
## <a name="odbc-data-sources"></a>Orígenes de datos ODBC  
 Una diferencia importante entre el código de ADO de secuencias de comandos y secuencias de comandos no es el origen de datos ODBC, si usa. Para las aplicaciones que no son secuencias de comandos, puede crear un DSN de usuario en el Administrador de orígenes de datos ODBC. Para los scripts que se ejecutan en IIS, debe crear un DSN de sistema; en caso contrario, las secuencias de comandos no reconocerá el origen de datos que creó. Esto se aplica a cualquier aplicación de secuencias de comandos de ADO con el proveedor Microsoft OLE DB para ODBC a través de Microsoft IIS.  
  
## <a name="referencing-the-ado-library"></a>Hacer referencia a la biblioteca ADO  
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
