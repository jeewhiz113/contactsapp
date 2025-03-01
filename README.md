Section 1: Deployment of the FE to GCP

Part 1:
Step 1: Enable the Cloud Storage API (to store the FE built files)
Step 2: Enable the Cloud DNS API (Domain Name System) to traffic from a specified domain name to cloud storage
Step 3: Enable Identity Access Manage API, to allow the public to access the storage

Part 2: create a cloud storage bucket
Step 1: Create Bucket in Cloud Storage
Step 2: Choose: Bucket Name (this will actas the public domain storage bucket e.g. yourdomain.com)
Step 3: Choose: region (close to your users)
Step 4: Choose: Storage class (standard)
Step 5: Choose: Access Control: Uniform access control (recommended)
Click Create
Step 6: Set Bucket to Public => Permission, click Grant Access => Add the following member: Principal: allUsers and Role: Storage Object Viewer

Part 3: Upload React Build Files
Step 1: Go to bucket and upload the contents of the /build folder and make sure the index.html is at the root level.

Part 4: Set the default Page:
Step 1: In Bucket > Edit Website Configuration > Main page: index.html and 404 Page: index.html
Step 2: Add "homepage": ".", to the package.json file so that react will mount the generated content to the id=root div.

Part 5: Accessing the website via Public URL (Note that if we want to connect to a custom domain name, we go to step 6)
Step 1: https://storage.googleapis.com/<bucket_name>/index.html
Optional: If you want the bucket to serve your app directly without typing /index.html, rename your index.html to index and update it again.

Part 6: Custom Domain (Cloud DNS, this step is only needed when you have a domain name registered)
If you want to connect a domain:

1. Go to Clound DNS.
2. Create a DNS Zone: Zone Name: yourdomain DNS Name: yourdomain.com Type: Public
3. Create an A Record: Type: A IPv4 Address: (34, 102, 136, 180) Google's LB IP for static websites
4. add CNAME if you have www.yourdomain.com
