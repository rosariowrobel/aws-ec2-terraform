# AWS EC2 Terraform Deployment

Este repositorio contiene los archivos necesarios para desplegar una aplicación web estática en una instancia EC2 utilizando **Terraform**. El proyecto incluye la configuración de una infraestructura mínima en AWS y el despliegue de una aplicación web simple servida por **Nginx**.

---

## **Contenido del Repositorio**

```
aws-ec2-terraform/
├── index.html         # Archivo HTML de la aplicación
├── style.css          # Archivo CSS de la aplicación
├── script.js          # Archivo JavaScript de la aplicación
├── main.tf            # Configuración de Terraform
├── README.md          # Documentación del proyecto
```

---

## **Descripción del Proyecto**

Este proyecto utiliza **Terraform** para gestionar la infraestructura en AWS y consta de los siguientes componentes:
1. **VPC** con una **Subnet pública**.
2. **Internet Gateway** para permitir tráfico externo.
3. **Grupo de seguridad** que permite tráfico HTTP (puerto 80) y SSH (puerto 22).
4. **Instancia EC2** que sirve una aplicación estática usando **Nginx**.

---

## **Requisitos Previos**

Antes de empezar, asegurate de tener instalado:
1. **Terraform** (versión 1.5.0 o superior).
2. Credenciales configuradas para AWS en tu máquina local (pueden ser con `aws configure` o variables de entorno).
3. Una clave SSH (`.pem`) para conectarte a la instancia EC2.

---

## **Iniciar el Proyecto**

### **1. Clonar el Repositorio**

```bash
git clone https://github.com/rosariowrobel/aws-ec2-terraform.git
cd aws-ec2-terraform
```

### **2. Configurar Terraform**

Inicializá Terraform para descargar los proveedores necesarios:

```bash
terraform init
```

### **3. Revisar la Configuración**

Podés revisar qué recursos se crearán con:

```bash
terraform plan
```

### **4. Aplicar la Configuración**

Ejecutá el siguiente comando para crear la infraestructura:

```bash
terraform apply
```

Confirmá escribiendo `yes` cuando se te solicite.

### **5. Conectar a la Instancia EC2**

Usá la dirección IPv4 pública de la instancia para conectarte vía SSH:

```bash
ssh -i "mi-clave-ec2.pem" ec2-user@<IPv4 pública>
```

### **6. Transferir los Archivos de la Aplicación**

Subí los archivos de la aplicación a la instancia:

```bash
scp -i "mi-clave-ec2.pem" ./index.html ./style.css ./script.js ec2-user@<IPv4 pública>:/home/ec2-user/
```

Luego, movelos al directorio de Nginx:

```bash
sudo mv /home/ec2-user/index.html /home/ec2-user/style.css /home/ec2-user/script.js /usr/share/nginx/html/
```

### **7. Verificar el Despliegue**

Abrí tu navegador y accedé a:

```
http://<IPv4 pública>
```

---

## **Capturas de Pantalla**

1. **Estado de la instancia EC2 en AWS:** Instancia `AppServer` en estado `Running`.
2. **Reglas del Grupo de Seguridad:** Reglas de entrada configuradas para los puertos 22 y 80.
3. **Conexión SSH Exitosa:** Terminal mostrando la conexión a la instancia.
4. **Aplicación Desplegada:** Navegador mostrando la página web.
