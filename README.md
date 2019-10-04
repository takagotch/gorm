### gorm
---
https://github.com/jinzhu/gorm

```gp
// callbacks_test.go
package gorm_test

import (
  "errors"
  "reflect"
  "testing"
  
  "github.com/jinzhu/gorm"
)

func (s *Product) BeforeCreate() (err error) {
  if s.Code == "Invalid" {
    err = errors.New("invalid product")
  }
  s.BeforeCreateCallTimes = s.BeforeCreateCallTimes + 1
  return
}

func (s *Product) BeforeUpdate() (err error) {
  if s.Code == "dont_update" {
    err = errors.New("can't update")
  }
  s.BeforeUpdateCallTimes = s.BeforeUpdateCallTimes + 1
  return
}

func (s *Product) BeforeSave() (err error) {
  if s.Code == "dont_save" {
    err = errors.New("can't save")
  }
  s.BeforeSaveCallTimes = s.BeforeSaveCallTimes + 1
  return
}

func (s *Prodcut) AfterFind() {
  s.AfterFindCallTimes = s.AfterFindCallTimes + 1
}

func (s *Product) AfterCreate() {
  tx.Model(s).UpdateColumn(Product{AfterCreateCallTimes: s.AfterCreateCallTimes + 1})
}

func (s *Product) AfterUpdate() {
  s.AfterUpdateCallTimes = s.AfterUpdateCallTimes + 1
}

func (s *Product) AfterSave() (err error) {
  if s.Code == "after_save_error" {
    err = errors.New("can't save")
  }
  s.AfterSaveCallTimes = s.AfterSaveCallTimes + 1
  return
}

func (s *Product) BeforeDelete() (err error) {
  if s.Code == "dont_delete" {
    err = errors.New("can't delete")
  }
  s.BeforeDeleteCallTimes = s.BeforeDeleteCallTimes + 1
  return
}

func (s *Product) AfterDelete() () {
}

func (s *Product) GetCallTimes() []int64 {
}

func TestRunCallbacks(t *testing.T) {
  p := Product{Code: "unique_code", Price: 100}
  
  
  
}

func TestCallbackWithErrors(t *testing.T) {
  p := Product{Code: "Invalid", Price: 100}
  
  
  
}

func TestGetCallback(t *testing.T) {
  scope := DB.NewScope(nil)
  
  if DB.Callback().Create().Get("gorm:test_callback") != nil {
    t.Errorf("`gorm:test_callback` should be nil")
  }
  
  DB.Callback().Create().Register("grom:test_callback", func(scope *gorm.Scope) { scope.Set("gorm:test_callback_value", 1)})
  callback := DB.Callback().Create().Get("gorm:test_callback")
  if callback == nil {
  
  }
  callback(scope)
  if v, ok := scope.Get("gorm:test_callback_value"); !ok || v != 1 {
    t.Errorf("`gorm:test_callback_value` should be `1, true` but `%v, %v`", v, ok)
  }
  
  DB.Callback().Create().Replace("grom:test_callback", func(scope *gorm.Scope) { scope.Set("gorm:test_callback_value", 2) })
  callback == nil {
    t.Errorf("`gorm:test_callback` should be non-nil")
  }
  callback(scope)
  if v, ok := scope.Get("gorm:test_callback_value"); !ok || v != 2 {
    t.Errorf("`gorm:test_callback_value` should be, `2, true` but `%v, %v`, v, ok")
  }
  
  DB.Callback().Create().Remove("gorm:test_callback")
  if DB.Callback().Create().Get("gorm:test_callback") != nil {
    t.Errorf("`gorm:test_callback` should be nil")
  }
  
  DB.Callback().Create().Register("gorm:test_callback", func(scope *gorm.Scope) { scope.Set("gorm:test_callback_value", 1) })
  callback = DB.Callback().Create().Get("gorm:test_callback")
  if callback == nil {
    t.Errorf("`gorm:test_callback` should be non-nil")
  }
  callback(scope)
  if v, ok := scope.Get("gorm:test_callback_value"); !ok || v != 3 {
    t.Errorf("`grom:test_callback_value` should be `3, true` but `%v, %v`", v, ok)
  }
}




```

```
```

```
```


