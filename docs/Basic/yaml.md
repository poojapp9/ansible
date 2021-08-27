# YAML

* Full form **YAML Ain't Markup Language**
* YAML is Data Serialization Language
* File Extensions
    * `.yaml`
    * `.yml`
* It is human readable and easy to write
* YAML uses line separation and indentation used to store data structure
---

## Writing YAML

### Key-Value Pair

:   Syntax: - `key: value`

    ```yaml
    app: "user-authentication"
    port: 9000
    version: 1.7
    ```

---

### Comments

:   Syntax: - `# Comment`

    ```yaml
    # Sinble Line Comment
    app: "user-authentication"
    port: 9000
    version: 1.7
    ```

---

### Objects

:   We can group this in object using spacing

    ```yaml
    microservice: # Object for Grouping
        # Sinble Line Comment
        app: "user-authentication"
        port: 9000
        version: 1.7
    ```

---

### list

If we have multiple `microservices` then we can list using -

:   **{++1: list of Objects grouping++}**
:
        ```yaml
        microservice: # Object for Grouping
        -   app: "user-authentication"
            port: 9000
            version: 1.7
        -   app: "shopping-cart"
            port: 9002
            version: 1.9
       ```

:   **{++2: list of simple values (list of just microservice names)++}**
        ```yaml
        microservice: # Object for Grouping
        -   user-authentication
        -   shopping-cart
        ```

:   **{++3: list of lists (we can create list of list using)++}**
    
:   - 3.1. first method using `-`
        ```yaml
        microservice: # Object for Grouping
        -   app: "user-authentication"
            port: 9000
            version: 1.7
        -   app: "shopping-cart"
            port: 9002
            version:
            -    1.9
            -    2.0
            -    2.1
        ```
   
:   - 3.2. second method using `[]`
        ```yaml
        microservice: # Object for Grouping
        -   app: "user-authentication"
            port: 9000
            version: 1.7
        -   app: "shopping-cart"
            port: 9002
            version: [1.9, 2.0, 2.1]
        ```

---

### Booleans

:   We can also use boolean values express using `on/off, true/false, yes/no`
    ```yaml
    microservice: # Object for Grouping
    -   app: "user-authentication"
        port: 9000
        version: 1.7
        deployed: true
    ```

---

### String

:   **{++1: Mutli-Line String++}**

:   * 1st method
    ```yaml
    multiString: "this is multiline String\nand this is the next line\nnext line"    
    ```
    * 2nd method using `|`
    ```yaml
    multiString: |
        this is multiline String
        and this is the next line
        next line
    ```

:   **{++2: Single-Line Sting++}**
    
:   * 1st method
    ```yaml
    multiString: "this is a single line String, that should be all on one line. some other stuff"    
    ```
    * 2nd method using `>`
    ```yaml
    multiString: >
        this is a single line String, 
        that should be all on one line. 
        some other stuff
    ```
---

### Placeholders
Values replaced from template generator using `{{ }}`
:   
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
        name: {{ .Values.service.name }}
    spec:
        selector:
            app: {{ .Values.service.app }}
        ports:
        -   protocol: TCP
            port: {{ .Values.service.port }}
            targetPort: {{ .Values.service.targetport }}
    ```

### Multiple YAML Files
Multiple YAML Documents in Single File usign ` --- `
:   
```yaml
apiVersion: v1
kind: Pod
metadata:
    name: nginx
    labels:
        app: nginx
    spec:
        containers:
        -   name: nginx-container
            image: nginx
            ports:
            -   containerPort: 80
            volumeMounts:
            -   name: nginx-vol
                mountPath: /usr/nginx/html
        -   name: sidecar-container
            image: some-image
            command: ["/bin/bash"]
            args: ["-c", "echo Hello from the sidecar-container; sleep 300"]
---
apiVersion: v1
kind: Service
metadata:
    name: {{ .Values.service.name }}
spec:
    selector:
        app: {{ .Values.service.app }}
    ports:
    -   protocol: TCP
        port: {{ .Values.service.port }}
        targetPort: {{ .Values.service.targetport }}
```

---

### Kubernetes YAML File Example
:   
```yaml
apiVersion: v1
kind: Pod
metadata:
    name: nginx
    labels:
        app: nginx
    spec:
        containers:
        -   name: nginx-container
            image: nginx
            ports:
            -   containerPort: 80
            volumeMounts:
            -   name: nginx-vol
                mountPath: /usr/nginx/html
        -   name: sidecar-container
            image: some-image
            command: ["/bin/bash"]
            args: ["-c", "echo Hello from the sidecar-container; sleep 300"]
```