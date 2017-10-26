---
title: "Método getEncrypt (SQLServerDataSource) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- getEncrypt Method (SQLServerDataSource)
apilocation:
- getEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 1cdb12dd-6e6f-4bbd-8f5f-9e630f3ee2c9
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c8edaf27e2c08b1738d8dedc3e059c0fecb5043b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getencrypt-method-sqlserverdatasource"></a>Método getEncrypt (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un **booleano** valor que indica si está habilitada la propiedad de cifrado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getEncypt()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si cifrar está habilitada. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Comentarios  
 Si la propiedad encrypt se establece en **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] garantiza que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] utiliza el cifrado SSL para todos los datos enviados entre el cliente y el servidor si el servidor tiene instalado un certificado.  
  
 Si la propiedad de cifrado se no se especifica o se establece en **false**, el controlador no aplicará el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] para admitir el cifrado SSL. Si el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] instancia no está configurada para exigir el cifrado SSL, se establece una conexión sin cifrado. Si el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] instancia está configurada para exigir el cifrado SSL, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] configurará automáticamente y habilitar el cifrado SSL cuando se ejecuta correctamente en configura la máquina Virtual Java (JVM), o bien se ha finalizado la conexión y el controlador generará un error. Si no se establece la propiedad de cifrado, el [getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md) método devuelve el valor predeterminado de **false**.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

