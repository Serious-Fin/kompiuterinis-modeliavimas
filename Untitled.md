history
    1  pwd
    2  exit
    3  pwd
    4  exit
    5  ls
    6  mkdir ex1
    7  ls
    8  mv main_mpi.py ex1/
    9  ls
   10  cd ex1
   11  ls
   12  pwd
   13  module load openmpi
   14  mpirun --version
   15  python3 --version
   16  python3 -m venv .venv
   17  ls
   18  ls -la
   19  source .venv/bin/activate
   20  ls
   21  which python
   22  python -m pip install numpy
   23  python -m pip install mpi4py
   24  ls
   25  ls -la
   26  ls
   27  vim job.sh
   28  ls
   29  sbatch job
   30  sbatch job.sh
   31  squeue
   32  squeue -j 243951
   33  squeue
   34  ls
   35  vim slurm-243951.out
   36  ls
   37  cp job.sh test.sh
   38  vim test.sh
   39  sbatch test.sh
   40  ls
   41  vim slurm-243952.out
   42  rm slurm-243951.out
   43  ls
   44  rm slurm-243952.out
   45  vim test.sh
   46  sbatch test.sh
   47  ls
   48  vim slurm-243953.out
   49  rm slurm-243953.out
   50  ls
   51  vim test.sh
   52  sbatch test.sh
   53  ls
   54  vim slurm-243954.out
   55  rm slurm-243954.out
   56  ls
   57  vim job.sh
   58  sbatch job.sh
   59  squeue
   60  ls
   61  vim slurm-243955.out
   62  ls
   63  squeue
   64  exit
   65  ls
   66  cd ex1
   67  ls
   68  rm pixels.npy
   69  rm slurm-243955.out
   70  rm main_mpi.py
   71  exit
   72  ls
   73  cd ex1/
   74  ls
   75  vim main_mpi.py
   76  vim job.sh
   77  squeue
   78  sbatch job.sh
   79  squeue
   80  ls
   81  squeue
   82  ls
   83  squeue
   84  ls
   85  squeue
   86  ls
   87  squeue
   88  ls
   89  squeue
   90  ls
   91  squeue
   92  ls
   93  squeue
   94  ls
   95  squeue
   96  ls
   97  vim slurm-244176.out
   98  exit
   99  ls
  100  cd ex1/
  101  ls
  102  rm main_mpi.py
  103  rm pixels.npy
  104  ls
  105  rm slurm-244176.out
  106  exit
  107  cd ex1/
  108  ls
  109  squeue
  110  sbatch job.sh
  111  squeue
  112  ls
  113  vim main_mpi.py
  114  sbatch job.sh
  115  squeue
  116  ls
  117  rm pixels.npy
  118  ls
  119  squeue
  120  ls
  121  vim slurm-244190.out
  122  exit
  123  squeue
  124  cd ex1/
  125  ls
  126  pwd
  127  ls
  128  mkdir ex2
  129  exit
  130  cd /scratch/lustre/home/augr3377/ex2
  131  ls
  132  module load openmpi
  133  export LD_LIBRARY_PATH="$(mpicc --showme:libdirs):${LD_LIBRARY_PATH:-}"
  134  sbatch job.sh
  135  squeue -j 248255
  136  ls
  137  cat slurm-248255.out
  138  python3 -m venv .venv
  139  ls
  140  ls -la
  141  cd ..
  142  cd ex1
  143  ls
  144  ls -la
  145  cd ..
  146  cd ex2
  147  ls
  148  source .venv/bin/activate
  149  MPICC=mpicc pip install --no-cache-dir --no-binary=mpi4py -r requirements.txt
  150  ls
  151  rm slurm-248255.out
  152  sbatch job.sh
  153  ls
  154  ls slurm-248256.out
  155  cat slurm-248256.out
  156  deactivate
  157  history