# proposalsampler
Experimental project. For given proposal or equation it generate its implementation (context or sample space $\Omega$ or model (like model for theory in logic therms))
at which this proposal (or equation) is true.
For example below, given the sent "abelian(G) \\and subgroup(H, G,) => abelian(H)", the program will generate some groups (described with they generators (like in GAP)) for G, H, at which this proposal is true (i.e. $\Omega = {\{H_{i}, G_{i}\} | where i \leq n}$ where $n$ is count of samples to be generated).
Only part of that "arguments" of the proposal can be given ($\Theta$) such that only remained part (\Psi) ought to be generated (so $\Omega = \Theta + \Psi$).  
The main idea is that such samples can give you better understanding of a proposal itself, especially if such proposal have been taken from some abstract math theory. 

##### sampling proposals:

```
from tokentranslator.db_models.model_main import TokenizerDB
from tokentranslator.env.clause.clause_main import Clause

model = TokenizerDB()

# switch to clauses db:
model.change_dialect_db("cs")

clause = Clause("abelian(G) \\and subgroup(H, G,) => abelian(H)", db=model)
clause.parser.parse()

# now import and use sampling:
from proposalsampler.sampling.slambda.tests_slambda_main import test_ventries 
from proposalsampler.sampling.slambda import slambda_main as sm

# for this example test_ventries[3] is init data for proposal clause:
test_ventries[3] =
{'G': ('(1,4)(2,3)', '(1,3)(2,4)'),
 "['s', 1, 0, 0]": True,
 "['s', 1, 1, 0]": True,
 'idd': "['s']",
 'successors_count': 0}

# so group G is given but group H is not, and must be found
# during sampling:
sampler = sm.Sampler(clause.net_out, test_ventries[3])

sampler.run()
# if successors found, they entries would look like:

{'G': ('(1,4)(2,3)', '(1,3)(2,4)'),  'H': ('(1,3)(2,4)', '(1,4)(2,3)')", ['s', 1, 1, 0]": True, "['s', 1, 0, 0]": True, 'idd': "['s', 4, 3, 0]", 'successors_count': 0, 'checked_nodes': ["['s']", "['s', 1]", "['s', 1, 1, 0]", "['s', 1, 0, 0]", "['s', 0, 0]"], 'failure_statuses': {}, 'parent_idd': "['s', 4, 3]", "['s']": True, "['s', 0, 0]": True, "['s', 1]": True}

# so group H found and in this case H = Group('(1,3)(2,4)', '(1,4)(2,3)') (= G but proposal is still holding) 
# if no results were generated, try run again.
```

##### sampling equations:
```
>>> e = Equation("f(a*x+b*y)=a*f(x)+b*f(y)")
>>> e.parser.parse()
>>> e.sampling.sympy.sampling_vars()
>>> # or e.sampling.sympy.sampling_subs()

>>> e.sampling.sympy.show_rand()
>>> # or "".join(e.eq_tree.flatten('rand_sympy'))

sin(0.243*0.570+0.369*0.078)=0.243*sin(0.570)+0.369*sin(0.078)
```
### Requirements
```
pip install -r requirements.txt

### Installation and running
```
pip install proposalsampler

### GUI:
There is also a GUI for this project at <br/>
https://github.com/tokentranslator-group/tokentranslator-gui

### Tests:
see `tests/test_list.txt`

### References:
##### Sampling:
Probabilistic Models of Cognition: https://probmods.org/

(eng: George Pólya: Mathematics and Plausible Reasoning, Princeton University Press 1954, 2 volumes (Vol. 1: Induction and Analogy in Mathematics, Vol. 2: Patterns of Plausible Inference)
(ru: Джордж Пойа: Математика и правдоподобные рассуждения)