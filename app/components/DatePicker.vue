<template>
  <div class="datepicker">
      <div class="panel panel-default">
          <div class="panel-heading">
              <div class="panel-title">Date Controls</div>
                <div class="panel-body">
                  <div class="row">
                    <div class="col-md-12">
                    <div class="form-group form-group-default input-group col-sm-12">
                      <label>Check In</label>
                      <input type="email" class="form-control" placeholder="Pick a date" id="datepicker-component2">
                      <span class="input-group-addon">
                        <i class="fa fa-calendar"></i>
                      </span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>       
    </div>
  </div>
</template>

<script>
export default {
  name: 'datepicker',
 data () {
    return {

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="sass" scoped>
  .panel {
    margin: 200px auto;
    width: 50%;
    background-color: rgba(255,255,255,0.4);
  }
</style>