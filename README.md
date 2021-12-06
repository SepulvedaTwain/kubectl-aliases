# kubectl-aliases
Some usefull kubectl (and other kubernetes releated) aliases, making it less painfull to type the whole command.


function kg(){
        resource=$1
        namespace=$2
        if [ -z "$namespace" ]
        then
                sudo kubectl get $resource
        else
                sudo kubectl get $resource -n $namespace
        fi
}
function kgp(){
        namespace=$1
        if [ -z "$namespace" ]
        then
                sudo kubectl get pods
        else
                sudo kubectl get pods -n $namespace
        fi
}
function wkgp(){
        namespace=$1
        if [ -z "$namespace" ]
        then
                watch sudo kubectl get pods
        else
                watch sudo kubectl get pods -n $namespace
        fi

}
function ktn(){
        node_name=$1
        if [ -z $node_name ] ;
        then
                echo "no node provided.. exiting.."
        else
                sudo kubectl taint nodes $node_name key1=value1:NoSchedule
        fi
}
function krtn(){
        node_name=$1
        if [ -z $node_name ] ;
        then
                echo "no node provided.. exiting.."
        else
                sudo kubectl taint nodes $node_name key1-
        fi
}


# Kubernetes aliases

alias k='sudo kubectl'
alias kubectl='sudo kubectl'

# Helm aliases

alias h3='sudo helm3'
alias h3i='sudo helm3 install'
alias h3d='sudo helm3 delete'

# Docker aliases

alias dps='sudo docker ps'
alias di='sudo docker images'
alias dig='sudo docker images | grep -i '

#kubectl & helm bash completion
source <(kubectl completion bash)
complete -F __start_kubectl k
source <(helm completion bash)

