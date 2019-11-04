# Security (15% of exam)

## Content may include the following:

* Describe the process of signing an image
* Demonstrate that an image passes a security scan
* Enable Docker Content Trust
* Configure RBAC in UCP
* Integrate UCP with LDAP/AD
* Demonstrate creation of UCP client bundles
* Describe default engine security
* Describe swarm default security
* Describe MTLS
* Identity roles
* Describe the difference between UCP workers and managers
* Describe process to use external certificates with UCP and DTR

## Questions:

<details><summary>What is DCT?</summary>
<p>

```
Through DCT, image publishers can sign their images and image consumers can ensure that the images they use are signed.
```
</p>
</details>



<details><summary>What is DCT stand for?</summary>
<p>

```
Docker Content Trust
```
</p>
</details>



<details><summary>What is the command to generate delegation keys?</summary>
<p>

```
docker trust generate key
```
</p>
</details>



<details><summary>How to load if you have any existing keys?</summary>
<p>

```
docker trust key load
```
</p>
</details>


<details><summary>How to sign a particular tag and push it up to the registry?</summary>
<p>

```
docker trust sign dtr.example.com/admin/demo:1
```
</p>
</details>



<details><summary>How to enable docker content trust so that you can sign images automatically when you use docker push?</summary>
<p>

```
export DOKCER_CONTENT_TRUST=1
```
</p>
</details>



<details><summary>How to inspect remote trusted data for a tag?</summary>
<p>

```
docker trust inspect
```
</p>
</details>



<details><summary>How to remove remote trusted data for a tag?</summary>
<p>

```
docker trust revoke
```
</p>
</details>



<details><summary>What is a grant?</summary>
<p>

```
A grant defines who has how much access to set of resources
```
</p>
</details>



<details><summary> What is the subject?</summary>
<p>

```
A subject can be user, team, organization and is granted a role for set of resources
```
</p>
</details>



<details><summary> What is the role?</summary>
<p>

```
A role is a set of permitted API operations that you can assign to a specific subject and collection by using a grant
```
</p>
</details>



<details><summary> What is a Client Bundle?</summary>
<p>

```
A client bundle is a group of certificates downloadable directly from the Docker Universal Control Plane (UCP) user interface within the admin section for “My Profile”. 
This allows you to authorize a remote Docker engine to a specific user account managed in Docker EE, absorbing all associated RBAC controls in the process. You can now execute docker swarm commands 
from your remote machine that take effect on the remote cluster.
```
</p>
</details>



<details><summary>What is the easiest way to access or control the UCP?</summary>
<p>

```
Client Bundle
```
</p>
</details>



<details><summary>What is the kernel feature that isolates the processes running in different containers?</summary>
<p>

```
Namespaces
```
</p>
</details>



<details><summary>Which kernel feature limits the resources used by docker containers?</summary>
<p>

```
Control Groups
```
</p>
</details>



<details><summary>What is the kernel feature that needed extra configuration?</summary>
<p>

```
user
```
</p>
</details>


<details><summary>Docker swarm should be secure by default?</summary>
<p>

```
yes
```
</p>
</details>
