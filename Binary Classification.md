# Binary Classification

## Modules for various tasks

The first function creates the pipeline for normalization and grid search based on conditions specified by the user in the control panel.

```
def create_pipeline(norm, model):
    if norm == 1:
        scale = StandardScaler()
        pipe = Pipeline([('norm', scale), ('reg', model)])
    elif norm == 2:
        scale = MinMaxScaler()
        pipe = Pipeline([('norm', scale), ('reg', model)])
    else:
        pipe = Pipeline([('reg', model)])
    return pipe
```

The second function performs forward feature selection and returns the indices of best features.

```
def select_features(model, X_train, Y_train, selection,
                    score_criteria, see_details, norm=0):
    pipe = create_pipeline(norm, model)
    sfs = SequentialFeatureSelector(pipe,
                                    forward=selection,
                                    k_features='best',
                                    scoring=score_criteria,
                                    verbose=see_details)
    sfs = sfs.fit(X_train, Y_train)
    return list(sfs.k_feature_idx_)
```

This function performs grid search for the provided parameter grid and returns the best model object.

```
def run_model(model, param_grid, X_train, Y_train,
              X, Y, score_criteria, folds,
              see_details, norm=0):
    pipe = create_pipeline(norm, model)
    model_grid = GridSearchCV(pipe,
                              param_grid,
                              cv=folds,
                              scoring=score_criteria,
                              verbose=see_details)
    model_grid.fit(X_train, Y_train)
		pipe = create_pipeline(norm, model_grid.best_estimator_)
    return model_grid.best_estimator_
```

The last function calculates all the relevant metrics for the best hyper-parameter combination and returns a pandas series of these metrics.

```
def get_model_eval(model, X_train, Y_train, X_test, Y_test):
    cm = confusion_matrix(Y_test, model.predict(X_test))
    t1, f1, t0, f0 = cm[1, 1], cm[1, 0], cm[0, 0], cm[0, 1]
    precision = precision_score(Y_test, model.predict(X_test))
    recall = recall_score(Y_test, model.predict(X_test))
    return pd.Series([model,
                      (t1 + t0) / (t1 + t0 + f1 + f0),
                      precision,
                      recall,
                      2 * precision * recall / (precision + recall),
                      -1 if type(model.steps[1][1]) == RidgeClassifier else roc_auc_score(Y_test, model.predict_proba(X_test)[:, 1])])
```

## Global Hyper-parameter Dictionary (MAKE MODIFICATIONS HERE)

This is the global dictionary for various model parameters for all the models in this module. Some default set of values have been populated in the code for typical ranges based on the cancer dataset. This dictionary contains some of the key hyper-parameters for each model and it is not exhaustive. Users are encouraged to visit scikit-learn documentation to get a list of all the parameters and add to the below dictionary according to their requirements.

```
# Global model paramater grid dictionary------------------------------------
# Change your hyperparameter ranges for grid search in this section
PARAM_DICT = {
  LogisticRegression: {
    'reg__tol': [1e-2, 1e-4, 1e-6],
    'reg__fit_intercept': [True, False],
    'reg__penalty': ['l1', 'l2']
  },
  RidgeClassifier: {
    'reg__alpha': [0.1, 1, 100],
    'reg__copy_X': [True, False],
    'reg__fit_intercept': [True, False],
    'reg__tol': [0.1, 1],
    'reg__solver': ['auto', 'svd', 'cholesky', 'lsqr',
      'sparse_cg', 'sag', 'saga'
    ]
  },KNeighborsClassifier: {
    'reg__n_neighbors': [5, 30, 100]
  },
  GaussianNB: {
  },DecisionTreeClassifier: {
    'reg__max_depth': [5, 10, 20],
    'reg__max_features': [0.3, 0.7, 1.0],
    'reg__max_leaf_nodes': [10, 50, 100],
    'reg__splitter': ['best', 'random']
  },BaggingClassifier: {
    'reg__bootstrap': [True, False],
    'reg__bootstrap_features': [True, False],
    'reg__max_features': [0.3, 0.7, 1.0],
    'reg__max_samples': [0.3, 0.7, 1.0],
    'reg__n_estimators': [10, 50, 100]
  },
  RandomForestClassifier: {
    'reg__bootstrap': [True, False],
    'reg__max_depth': [5, 10, 20],
    'reg__max_features': [0.3, 0.7, 1.0],
    'reg__max_leaf_nodes': [10, 50, 100],
    'reg__min_impurity_decrease': [0, 0.1, 0.2],
    'reg__n_estimators': [10, 50, 100]
  },SVC: {
    'reg__C': [10 ** -3, 1, 1000],
    'reg__kernel': ['linear', 'poly', 'rbf'],
    'reg__shrinking': [True, False],
    'reg__probability': [True]
  },GradientBoostingClassifier: {
    'reg__learning_rate': [0.1, 0.2, 0.5],
    # 'reg__loss': ['ls', 'lad', 'huber', 'quantile'],
    'reg__max_depth': [10, 20, 50],
    'reg__max_features': [0.5, 0.8, 1.0],
    'reg__max_leaf_nodes': [10, 50, 100],
    'reg__min_impurity_decrease': [0, 0.1, 0.2],
    'reg__min_samples_leaf': [5, 10, 20],
    'reg__min_samples_split': [5, 10, 20],
    'reg__n_estimators': [10, 50, 100]
  },
  XGBClassifier: {
    'reg__booster': ['gbtree', 'gblinear', 'dart'],
    'reg__learning_rate': [0.2, 0.5, 0.8],
    'reg__max_depth': [5, 10, 20],
    'reg__n_estimators': [10, 50, 100],
    'reg__reg_alpha': [0.1, 1, 10],
    'reg__reg_lambda': [0.1, 1, 10],
    'reg__subsample': [0.3, 0.5, 0.8],
    'reg__probability': [True]
  }}
```

## User Control Panel For Key Inputs (MAKE MODIFICATIONS HERE)

The inputs to the modules can be changed here. This is the control panel for this script where all the variables mentioned in the introduction can be altered to test various scenarios. Please refer to the comments to understand the variables.

```
# --------------------------------------------------------------------------
# USER CONTROL PANEL, CHANGE THE VARIABLES, MODEL FORMS ETC. HERE# Read data here, define X (features) and Y (Target variable)
data = datasets.load_breast_cancer()
X = pd.DataFrame(data['data'])
X.columns = data['feature_names']
Y = data['target']# Specify size of test data (%)
size = 0.3# Set random seed for sampling consistency
random.seed(100)# Set type of normalization you want to perform
# 0 - No Normalization, 1 - Min-max scaling, 2 - Zscore scaling
norm = 1# Mention all model forms you want to run
to_run = [DecisionTreeClassifier,
          BaggingClassifier,
          RandomForestClassifier,
          GradientBoostingClassifier,
          XGBClassifier,
          SVC,
          KNeighborsClassifier,
          RidgeClassifier,
          GaussianNB,
          LogisticRegression]# Specify number of crossvalidation folds
folds = 2# Specify model selection criteria
# Possible values are:
# 'accuracy'
# 'precision'
# 'recall'
# 'f1'
# 'roc_auc'score_criteria = 'accuracy'# Specify details of terminal output you'd like to see
# 0 - No output, 1 - All details, 2 - Progress bar
# Outputs might vary based on individual functions
see_details = 0
```

## Model Execution

This section iteratively finds the best set of the hyperparameters for each of the model specified by the user, calculates the metrics and populates results table for further analysis/experimentation.

```
# Model execution part, results will be stored in the dataframe 'results'
# Best model can be selected based on these criteria
results = pd.DataFrame(columns=['model', 'Accuracy', 'PrecisionLab1', 'RecallLab1',
                                'FMeasureLab1', 'AUC'])
X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=size)
for model in to_run:
    with warnings.catch_warnings():
        warnings.simplefilter('ignore')
        best_feat = select_features(model(), X_train, Y_train, True,
                                    score_criteria, see_details, norm)
        model = run_model(model(), PARAM_DICT[model],
                          X_train.iloc[:, best_feat],
                          Y_train,
                          X.iloc[:, best_feat], Y,
                          score_criteria, folds, see_details, norm)
        stats = get_model_eval(model, X_train.iloc[:, best_feat], Y_train,
                               X_test.iloc[:, best_feat], Y_test)
        stats.index = results.columns
        results = results.append(stats, ignore_index=True)print(results)
results['Form'] = [str(i).split()[-1].split('.')[-1] for i in to_run]
sb.lmplot('RecallLab1', 'Accuracy', hue='Form', data=results, fit_reg=False)
```

## Conclusion

![https://miro.medium.com/max/1128/1*bGtVlKC9_UflwbyPQo9xNQ.png](https://miro.medium.com/max/1128/1*bGtVlKC9_UflwbyPQo9xNQ.png)

In the case of the cancer patient detection, it would be very important to detect all the patients, in formal terms, to have the recall as high as possible for our model. From the above graph, we can observe that there are 3 models which are able to achieve perfect recall: Ridge classifier, logistic regression and support vector machine. In this scenario, the best way forward would be to pick the model with the highest accuracy among these models which is SVM. Similar to the example in regression notebook, the simpler models such as logistic regression and ridge classifier perform better than ensemble models.

I hope this module enables faster experimentation and provides an opportunity to build further customizations on top of it based on your needs!