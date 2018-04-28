---
title: Interfaz SQLXML | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7c67be98-efb5-446c-a0e3-ee67c43cb170
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a53f884d6cff364e30b110e05c311076459fdbd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlxml-interface"></a>Interfaz SQLXML
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El controlador JDBC ofrece compatibilidad con la API de JDBC 4.0, que presenta la interfaz java.sql.SQLXML. La interfaz SQLXML define métodos para interactuar y manipular datos XML. El **SQLXML** tipo de datos se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **xml** tipo de datos.  
  
 La interfaz SQLXML proporciona métodos para tener acceso al valor XML como un **cadena**, **lector** o **escritor**, o como un **flujo**. El valor XML también puede obtenerse a través de un **origen** o se establece como un **resultado**, que se utilizan con las API del analizador de XML, como Document Object Model (DOM), la API Simple para XML (SAX) y Streaming API for XML (StAX), como así como con XSLT transforma y XPath.  
  
## <a name="remarks"></a>Comentarios  
 La tabla siguiente describe los métodos definidos en la interfaz SQLXML:  
  
|Sintaxis del método|Descripción del método|  
|-------------------|------------------------|  
|[free() void](http://go.microsoft.com/fwlink/?LinkId=131685)|Este método libera el objeto SQLXML y los recursos que contiene.|  
|[InputStream getBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131754)|Devuelve un flujo de entrada para leer datos desde SQLXML.|  
|[Lector getCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131755)|Devuelve el **XML** datos como un objeto java.io.Reader o como una secuencia de caracteres.|  
|[T extiende getSource T de origen (clase\<T > sourceClass)](http://go.microsoft.com/fwlink/?LinkId=131756)|Devuelve un **origen** para leer el **XML** valor especificado por este **SQLXML** objeto.<br /><br /> **Nota:** el método getSource es compatible con los siguientes orígenes: javax.xml.transform.dom.DOMSource, javax.xml.transform.sax.SAXSource, javax.xml.transform.stax.StAXSource y java.io.InputStream.|  
|[Cadena getString()](http://go.microsoft.com/fwlink/?LinkId=131757)|Devuelve una representación de cadena de la **XML** valor designado por este objeto SQLXML.|  
|[OutputStream setBinaryStream()](http://go.microsoft.com/fwlink/?LinkId=131758)|Recupera una secuencia que puede utilizar para escribir el **XML** valor que representa este objeto SQLXML.|  
|[Sistema de escritura setCharacterStream()](http://go.microsoft.com/fwlink/?LinkId=131759)|Devuelve una secuencia que se va a usarse para escribir la **XML** valor que representa este objeto SQLXML.|  
|[T extiende resultado T setResult (clase\<T > resultClass)](http://go.microsoft.com/fwlink/?LinkId=131760)|Devuelve un **resultado** para la configuración de la **XML** valor especificado por este **SQLXML** objeto.<br /><br /> **Nota:** el método setResult es compatible con los siguientes orígenes: javax.xml.transform.dom.DOMResult, javax.xml.transform.sax.SAXResult, javax.xml.transform.stax.StaxResult y java.io.OutputStream.|  
|[void setString(String value)](http://go.microsoft.com/fwlink/?LinkId=131762)|Establece el valor XML designado por este objeto SQLXML en especificado **cadena** representación.|  
  
 Las aplicaciones pueden leer y escribir valores XML en o desde un objeto SQLXML solamente una vez.  
  
 Cuando se llama al método de free(), un objeto SQLXML deja de ser válido y no es legible ni grabable. Si la aplicación intenta invocar un método en ese objeto SQLXML distinto del método free(), se produce una excepción.  
  
 El objeto SQLXML pasa a ser legible ni modificable cuando la aplicación llama a cualquiera de los siguientes métodos de captador: getSource, getCharacterStream, getBinaryStream y getString.  
  
 El objeto SQLXML se convierte en grabable ni legibles cuando la aplicación llama a cualquiera de los siguientes métodos establecedores: setResult, setCharacterStream, setBinaryStream y setString.  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con datos XML](../../connect/jdbc/supporting-xml-data.md)  
  
  
