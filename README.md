# cloud_dataproc
Distributed Image Processing in Cloud Dataproc 


On GCP:
* create a development machine in Compute Engine
* On Compute Engine, 
    * Install Scala, sbt
    * Git clone https://github.com/GoogleCloudPlatform/cloud-dataproc
    * cd cloud-dataproc/codelabs/opencv-haarcascade -- BUILD Files
      * sbt assembly
* Create a GCS bucket and upload images for processing

* Create DataProc Cluster
  * gcloud config set dataproc/region global
  * gcloud dataproc clusters create ${MYCLUSTER} --bucket=${MYBUCKET} --worker-machine-type=n1-standard-2 --master-machine-type=n1-standard-2   

* Submit your job to Cloud Dataproc
  *gcloud dataproc jobs submit spark \
--cluster ${MYCLUSTER} \
--jar target/scala-2.10/feature_detector-assembly-1.0.jar -- \
gs://${MYBUCKET}/haarcascade_frontalface_default.xml \
gs://${MYBUCKET}/imgs/ \
gs://${MYBUCKET}/out/
