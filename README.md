# STEPS TO ACCESS WITH KUBEFLOW123


To access the central dashboard, you need to connect to the Istio gateway that provides access to the Kubeflow
Use the following command to set up port forwarding to the Istio gateway
command : kubectl port-forward svc/istio-ingressgateway 8080:80 -n istio-system

Kubeflow Dashboard will shown on browser and then we can look on navigation bar we will see

- Home
- Pipelines
- Notebook Server
- Katib
- Artifact Store
- Manage Contributors


# Notebook Server 
Create a Jupyter notebook server and add a notebook

1. Click NEW SERVER on the Notebook Servers
2. Enter a name of notebook server
3. There is a image part that we have to select,by default already image are there but if you custom image we can kept
4. We can also mention CPU and Memory
5. We can Configure the volume
6. We can also set Persistant Volume for backup
7. We can also set GPU
8. Last We click on lunch to set a nootbook server

# When the notebook server is available, click Connect to connect to it.

After setup a notebook server,we will see jupyter notebook server on browser
In jupyter notebook,We tested image detection project
The main benefits of using notebbok is that we can create notebook containers or pods directly in the cluster, rather than locally on their workstations.

There are two ways to run pipeline in notebook
1. kale(Kubeflow Automated Pipeline Engine
 Using kale we can automatically run ml code to pipelines
2. Jupyter Nootbook
 - In this we manually have to run a python code and we also have to write code to run pipelines

We have tested both using kale as well as jupyter notebook.



## Pipelines

The Kubeflow Pipelines platform consists of:

    - A user interface (UI) for managing and tracking experiments, jobs, and runs.
    - An engine for scheduling multi-step ML workflows.
    - An SDK for defining and manipulating pipelines and components.
    - Notebooks for interacting with the system using the SDK.



# Kubeflow Pipeline UI

In Pipeline Ui we can look on navigation bar we wiil see
- Pipelines
- Experiments
- Artifacts
- Execution


We can upload pipelines using yaml,tar file, or from jupyter notebook it will create a pipelines directly.
while creating a pipeline every steps of pipelines it will create a pod in a cluster.

We can see logs of pods in pipeline ui.we don't have to go on cluster.


In pipeline state first we have to train then after predict a model and last print a model.



Experiments with the pipelines sample

# Set up an environments
1. Clone or download the Kubeflow Pipelines samples.
2. Install the Kubeflow Pipelines SDK.
3. Activate your Python 3 environmen
    For example:

      source activate mlpipeline
4. Choose and compile a pipeline

  Use the dsl-compile command to compile the pipeline that you chose:

dsl-compile --py [path/to/python/file] --output [path/to/output/tar.gz]

5. Deploy a pipeline


# Katib

Accessing the Katib UI

You can use the Katib user interface (UI) to submit experiments and to monitor your results. 

If you installed Katib as part of Kubeflow, you can access the Katib UI from the Kubeflow UI:

Open the Kubeflow UI. Check the guide to accessing the central dashboard.Click Katib in the left-hand menu.

Alternatively, you can set port-forwarding for the Katib UI service:

   -- kubectl port-forward svc/katib-ui -n kubeflow 8080:80
   
Then you can access the Katib UI at this URL:

     http://localhost:8080/katib/

Examples

Example using random algorithm

1. Download the example
   curl https://raw.githubusercontent.com/kubeflow/katib/master/examples/v1beta1/random-example.yaml --output random-example.yaml

2. Edit random-example.yaml and change the following line to use your Kubeflow user profile namespace
3. Deploy the example:
 - kubectl apply -f random-example.yaml
4. Check the experiment status:

### The output of the above 
     currentOptimalTrial:
        bestTrialName: random-example-smpc6ws2
        observation:
          metrics:
            - latest: "0.993170"
              max: "0.993170"
              min: "0.920293"
              name: Train-accuracy
            - latest: "0.978006"
              max: "0.978603"
              min: "0.959295"
              name: Validation-accuracy
        parameterAssignments:
          - name: lr
            value: "0.02889324678979306"
          - name: num-layers
            value: "5"
          - name: optimizer
            value: sgd
      runningTrialList:
        - random-example-26d5wzn2
        - random-example-98fpd29m
        - random-example-x2vjlzzv
      startTime: "2020-10-23T21:27:53Z"
      succeededTrialList:
        - random-example-n9c4j4cv
        - random-example-qfb68jpb
        - random-example-s96tq48v
        - random-example-smpc6ws2
      trials: 7
      trialsRunning: 3
      trialsSucceeded: 4

  



View the results of the experiment in the Katib UI:

    1. Open the Katib UI as described above.
    2. Click Hyperparameter Tuning on the Katib home page.
    3. Open the Katib menu panel on the left, then open the HP section and click Monitor
    4. You should be able to view the list of experiments
    5. Click the name of the experiment, random-example.
    6. There should be a graph showing the level of validation and train accuracy for various combinations of the hyperparameter values (learning rate, number of layers, and optimizer)


